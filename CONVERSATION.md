# Building a Long-Running Conversation with Tool Calling

A guide on architectural patterns for building agentic conversation systems that support multi-turn tool calling, derived from studying a production-grade implementation.

---

## 1. The Conversation Loop

The core of an agentic conversation is an **infinite loop** that alternates between calling the model and executing tools. The loop runs until the model produces a response with no tool calls, signaling it has finished its work.

```
while true:
  response = call_model(messages)
  append assistant message to messages

  if response has no tool calls:
    break

  execute tools from response
  append tool results to messages
```

This simple pattern enables the model to chain multiple tool calls across turns without returning to the user. The user submits a single message, and the loop may iterate many times before producing a final answer.

### Nesting the Loop

Wrap the loop inside a higher-level **session manager** that owns the full message history. The session manager handles user input, invokes the loop, and collects output. This separation keeps the agentic loop focused on model-tool interaction while the session layer manages lifecycle concerns like persistence, hooks, and user-facing events.

---

## 2. Tool Definition and Registration

Define tools as structured objects with:

- **Name and description** for the model to understand when to use the tool.
- **Input schema** (JSON Schema) for the model to generate valid arguments.
- **Execution handler** that performs the actual work and returns a result.
- **Permission rules** that determine whether the tool can run without user approval.
- **Concurrency metadata** indicating whether the tool is safe to run in parallel with others.

Maintain a **tool registry** that the system consults at two points: when building the API request (to list available tools) and when processing a response (to dispatch tool calls to the correct handler).

---

## 3. Tool Execution

When the model returns tool-use blocks in its response, the system must execute each one and feed results back as messages.

### Sequential vs. Parallel Execution

Not all tools are safe to run concurrently. A file-read tool is safe to parallelize; a file-write tool is not. Partition tool calls into **batches**:

- Group consecutive concurrency-safe tools into a single batch and run them in parallel.
- Isolate non-concurrent tools into their own batch and run them alone.

Execute batches in order, but tools within a concurrent batch run simultaneously.

### Streaming Tool Execution

In a streaming setup, tool-use blocks arrive incrementally. Rather than waiting for the full response, begin executing tools as soon as each tool-use block is complete. This overlaps model generation time with tool execution time, significantly reducing end-to-end latency.

### Result Format

Each tool result is a **user-role message** containing a `tool_result` content block that references the original `tool_use_id`. The model uses this ID to associate results with the calls it made. Accumulate all results and append them to the message list before the next model call.

---

## 4. Message Management

The message list is the system's primary state. Every interaction—user input, model output, tool results, system events—becomes a message appended to this list.

### Message Types

Internally, you may track more message types than the API supports:

- **User messages**: Human input and tool results.
- **Assistant messages**: Model output (text, thinking, tool calls).
- **System/meta messages**: Internal bookkeeping (permission events, progress updates, status).

### Normalization Before API Calls

The API has strict requirements (alternating user/assistant roles, tool-result pairing). Before each call, **normalize** the internal message list:

- Filter out display-only or internal messages.
- Merge consecutive messages of the same role.
- Ensure every tool-use block has a matching tool-result (insert synthetic results for any that are missing).
- Strip internal-only fields from tool inputs.

Keep the internal representation rich and the API-facing representation clean.

---

## 5. Context Window Management

Long-running conversations inevitably exceed the model's context window. A robust system needs multiple strategies, applied in stages.

### Proactive Compaction

Before hitting the limit, **summarize older messages** and replace them with a condensed version. Monitor token usage after each API call and trigger compaction when usage crosses a threshold (e.g., 80% of the window). This avoids ever hitting the hard limit during normal operation.

### Reactive Compaction

When the API returns a "prompt too long" error, perform emergency compaction:

1. First, try lightweight strategies (collapsing tool-result details, trimming large outputs).
2. If still too long, summarize the full conversation history.
3. Retry the API call with the compacted messages.

### Incremental Context Collapse

Rather than summarizing the entire history at once, collapse messages in **groups**. Archive older message groups into summaries while keeping recent messages intact. This preserves detail where it matters most (recent context) while freeing space from older turns.

### Message Snipping

For very large tool results (e.g., reading a large file), store the full content but mark it as **snippable**. On compaction, replace snipped content with a placeholder. Optionally, provide the model with a tool to retrieve snipped content on demand.

---

## 6. Streaming

Stream responses from the API using server-sent events. Process events incrementally:

- `message_start`: Initialize the assistant message.
- `content_block_start/delta/stop`: Accumulate text, thinking, or tool-use content.
- `message_delta`: Capture final metadata (stop reason, usage).
- `message_stop`: Finalize the message.

Use an **async generator** pattern so consumers can iterate over events as they arrive. This enables real-time UI updates and the streaming tool execution described earlier.

### Streaming Fallback

If streaming fails mid-response (e.g., server overload), fall back to a non-streaming request. Clean up any partial messages from the failed stream using **tombstone markers** that tell the UI to remove incomplete content.

---

## 7. Error Handling and Recovery

Errors in a long-running conversation must be handled gracefully to avoid losing accumulated work.

### API-Level Retries

Wrap API calls with **exponential backoff** for transient errors (rate limits, server overload). Cap retries and distinguish between retryable errors (429, 529) and permanent failures (400, 403).

### In-Loop Recovery

Some errors can be recovered within the conversation loop without surfacing to the user:

- **Prompt too long**: Trigger compaction and retry.
- **Max output tokens**: Escalate the token limit (e.g., 8K to 64K) and retry, or split the response across multiple turns. Cap recovery attempts to prevent infinite loops.
- **Tool execution failure**: Return the error as a tool result with an error flag. The model can then decide how to proceed (retry, try a different approach, or inform the user).

### Abort Handling

Support cancellation via an **abort controller** pattern. When the user interrupts:

1. Signal cancellation to any in-progress tool executions.
2. Collect results from tools that already completed.
3. Insert synthetic results for cancelled tools.
4. Append an interruption message so the model has context if the conversation resumes.

---

## 8. Turn Management

A "turn" is the full cycle from user input to final model response. Within a single turn, the model may iterate multiple times through the loop (calling tools and continuing).

### Continuation Decisions

After each loop iteration, decide whether to continue or exit:

1. **Tool calls present**: Continue — execute tools and loop.
2. **No tool calls, model says stop**: Exit — return the response to the user.
3. **Recovery needed**: Continue — apply recovery strategy and retry.
4. **Turn limit reached**: Exit — prevent runaway loops by capping iterations.

### Stop Hooks

Optionally run **stop hooks** after the model produces a response. These can:

- Force continuation (e.g., "the model forgot to run tests").
- Prevent continuation (e.g., "budget exhausted").

Stop hooks run before the exit decision, giving external logic a chance to influence the loop.

### Token Budgets

Track cumulative token usage across iterations. Set a **task budget** so the system can exit gracefully when it determines diminishing returns, rather than consuming unlimited resources.

---

## 9. State Management

Separate state into two categories:

### Session State (persists across all turns)

- **Message history**: The full conversation.
- **Cumulative usage**: Total tokens consumed.
- **Permission records**: Which tool calls were approved or denied.
- **File state cache**: Cached results from file reads for consistency.

### Turn State (reset each iteration of the loop)

- **Recovery counters**: How many times the system has retried within this turn.
- **Compaction tracking**: Whether compaction has been attempted.
- **Transition reason**: Why the loop continued (tool use, recovery, hook).
- **Output token overrides**: Any escalated limits for this iteration.

Keeping these separate prevents stale turn-level state from leaking across iterations and ensures session-level state accumulates correctly.

---

## 10. Permission and Safety

Every tool execution should pass through a **permission gate**:

1. Check the tool against the current permission mode (auto-approve, ask, deny).
2. Check tool-specific rules (e.g., "allow all file reads, ask for file writes").
3. If denied, record the denial and return it as a tool result so the model can adapt.
4. Accumulate denials for reporting to the session layer.

This prevents the model from taking destructive actions without user consent and gives the model feedback when it tries something disallowed.

---

## Summary of Key Patterns

| Pattern | Purpose |
|---|---|
| Infinite loop with break-on-no-tools | Enables multi-turn agentic behavior |
| Streaming tool execution | Overlaps model and tool latency |
| Message normalization | Bridges rich internal state and strict API format |
| Layered compaction | Manages context window without losing critical context |
| Exponential backoff with recovery | Handles transient and structural API errors |
| Turn-scoped vs. session-scoped state | Prevents state leakage across loop iterations |
| Permission gating at tool boundary | Maintains user control over side effects |
| Async generator architecture | Enables real-time streaming to consumers |
