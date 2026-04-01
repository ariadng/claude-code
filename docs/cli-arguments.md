# Claude Code CLI Arguments Reference

Complete reference for all CLI arguments, flags, and subcommands available in Claude Code.

## Usage

```
claude [prompt] [options]
claude <subcommand> [options]
```

---

## Global Options

### General

| Flag | Description |
|------|-------------|
| `-h, --help` | Display help for command |
| `-v, --version` | Output the version number |
| `-d, --debug [filter]` | Enable debug mode with optional category filtering (e.g., `"api,hooks"` or `"!1p,!file"`) |
| `--debug-file <path>` | Write debug logs to a specific file path (implicitly enables debug mode) |
| `--verbose` | Override verbose mode setting from config |

### Session Mode

| Flag | Description |
|------|-------------|
| `-p, --print` | Print response and exit (useful for pipes). Skips the workspace trust dialog. Only use in directories you trust. |
| `--bare` | Minimal mode: skip hooks, LSP, plugin sync, attribution, auto-memory, background prefetches, keychain reads, and CLAUDE.md auto-discovery. Sets `CLAUDE_CODE_SIMPLE=1`. Use explicit context flags (`--system-prompt`, `--add-dir`, `--mcp-config`, `--settings`, `--agents`, `--plugin-dir`) to provide context. |

### Output Configuration

| Flag | Description |
|------|-------------|
| `--output-format <format>` | Output format (only with `--print`): `text` (default), `json` (single result), or `stream-json` (realtime streaming) |
| `--input-format <format>` | Input format (only with `--print`): `text` (default) or `stream-json` (realtime streaming input) |
| `--json-schema <schema>` | JSON Schema for structured output validation. Example: `'{"type":"object","properties":{"name":{"type":"string"}},"required":["name"]}'` |
| `--include-hook-events` | Include all hook lifecycle events in the output stream (only with `--output-format=stream-json`) |
| `--include-partial-messages` | Include partial message chunks as they arrive (only with `--print` and `--output-format=stream-json`) |
| `--replay-user-messages` | Re-emit user messages from stdin back on stdout for acknowledgment (only with `--input-format=stream-json` and `--output-format=stream-json`) |

### Model & Effort

| Flag | Description |
|------|-------------|
| `--model <model>` | Model for the current session. Provide an alias (e.g., `sonnet` or `opus`) or a full model name (e.g., `claude-sonnet-4-6`). |
| `--effort <level>` | Effort level for the current session: `low`, `medium`, `high`, `max` |
| `--agent <agent>` | Agent for the current session. Overrides the `agent` setting. |
| `--fallback-model <model>` | Enable automatic fallback to specified model when default model is overloaded (only with `--print`) |
| `--betas <betas...>` | Beta headers to include in API requests (API key users only) |

### Session Management

| Flag | Description |
|------|-------------|
| `-c, --continue` | Continue the most recent conversation in the current directory |
| `-r, --resume [value]` | Resume a conversation by session ID, or open interactive picker with optional search term |
| `--fork-session` | When resuming, create a new session ID instead of reusing the original (use with `--resume` or `--continue`) |
| `--from-pr [value]` | Resume a session linked to a PR by PR number/URL, or open interactive picker with optional search term |
| `--session-id <uuid>` | Use a specific session ID for the conversation (must be a valid UUID) |
| `-n, --name <name>` | Set a display name for this session (shown in `/resume` and terminal title) |
| `--no-session-persistence` | Disable session persistence — sessions will not be saved to disk and cannot be resumed (only with `--print`) |

### Permissions

| Flag | Description |
|------|-------------|
| `--permission-mode <mode>` | Permission mode to use for the session. Choices depend on available modes. |
| `--dangerously-skip-permissions` | Bypass all permission checks. Recommended only for sandboxes with no internet access. |
| `--allow-dangerously-skip-permissions` | Enable bypassing permission checks as an option without it being enabled by default. Recommended only for sandboxes with no internet access. |

### Tools & MCP

| Flag | Description |
|------|-------------|
| `--allowedTools, --allowed-tools <tools...>` | Comma or space-separated list of tool names to allow (e.g., `"Bash(git:*) Edit"`) |
| `--tools <tools...>` | Specify the list of available tools. Use `""` to disable all, `"default"` to use all, or specify tool names (e.g., `"Bash,Edit,Read"`). |
| `--disallowedTools, --disallowed-tools <tools...>` | Comma or space-separated list of tool names to deny (e.g., `"Bash(git:*) Edit"`) |
| `--mcp-config <configs...>` | Load MCP servers from JSON files or strings (space-separated) |
| `--strict-mcp-config` | Only use MCP servers from `--mcp-config`, ignoring all other MCP configurations |
| `--mcp-debug` | **[DEPRECATED]** Use `--debug` instead. Enable MCP debug mode (shows MCP server errors). |

### System Prompts

| Flag | Description |
|------|-------------|
| `--system-prompt <prompt>` | System prompt to use for the session |
| `--system-prompt-file <file>` | Read system prompt from a file (hidden) |
| `--append-system-prompt <prompt>` | Append a system prompt to the default system prompt |
| `--append-system-prompt-file <file>` | Read system prompt from a file and append to the default system prompt (hidden) |

### Configuration & Settings

| Flag | Description |
|------|-------------|
| `--settings <file-or-json>` | Path to a settings JSON file or a JSON string to load additional settings |
| `--setting-sources <sources>` | Comma-separated list of setting sources to load (user, project, local) |
| `--add-dir <directories...>` | Additional directories to allow tool access to |
| `--plugin-dir <path>` | Load plugins from a directory for this session only (repeatable: `--plugin-dir A --plugin-dir B`) |
| `--agents <json>` | JSON object defining custom agents (e.g., `'{"reviewer": {"description": "Reviews code", "prompt": "You are a code reviewer"}}'`) |
| `--disable-slash-commands` | Disable all skills |
| `--ide` | Automatically connect to IDE on startup if exactly one valid IDE is available |
| `--chrome` | Enable Claude in Chrome integration |
| `--no-chrome` | Disable Claude in Chrome integration |

### Budget & Limits

| Flag | Description |
|------|-------------|
| `--max-turns <turns>` | Maximum number of agentic turns in non-interactive mode. Early exits after the specified number. (only with `--print`, hidden) |
| `--max-budget-usd <amount>` | Maximum dollar amount to spend on API calls (only with `--print`) |

### Worktree

| Flag | Description |
|------|-------------|
| `-w, --worktree [name]` | Create a new git worktree for this session (optionally specify a name) |
| `--tmux` | Create a tmux session for the worktree (requires `--worktree`). Uses iTerm2 native panes when available; use `--tmux=classic` for traditional tmux. |

### File Resources

| Flag | Description |
|------|-------------|
| `--file <specs...>` | File resources to download at startup. Format: `file_id:relative_path` (e.g., `--file file_abc:doc.txt file_def:img.png`) |

---

## Hidden / Advanced Options

These options are registered but hidden from `--help` output. They are used for internal features, SDK integration, deep links, and feature-gated functionality.

### SDK & Streaming

| Flag | Description |
|------|-------------|
| `-d2e, --debug-to-stderr` | Enable debug mode (output to stderr) |
| `--sdk-url <url>` | Use remote WebSocket endpoint for SDK I/O streaming (only with `-p` and `stream-json` format) |
| `--permission-prompt-tool <tool>` | MCP tool to use for permission prompts (only with `--print`) |
| `--enable-auth-status` | Enable auth status messages in SDK mode (default: false) |

### Thinking Configuration

| Flag | Description |
|------|-------------|
| `--thinking <mode>` | Thinking mode: `enabled` (equivalent to adaptive), `disabled` |
| `--max-thinking-tokens <tokens>` | **[DEPRECATED]** Use `--thinking` for newer models. Maximum thinking tokens (only with `--print`). |

### Task Budget

| Flag | Description |
|------|-------------|
| `--task-budget <tokens>` | API-side task budget in tokens (`output_config.task_budget`). Must be a positive integer. |

### Workload Tag

| Flag | Description |
|------|-------------|
| `--workload <tag>` | Workload tag for billing-header attribution (`cc_workload`). Process-scoped; set by SDK daemon callers. (only with `--print`) |

### Session Resume (Advanced)

| Flag | Description |
|------|-------------|
| `--resume-session-at <message id>` | When resuming, only messages up to and including the specified assistant message (use with `--resume` in print mode) |
| `--rewind-files <user-message-id>` | Restore files to state at the specified user message and exit (requires `--resume`) |
| `--prefill <text>` | Pre-fill the prompt input with text without submitting it |

### Deep Link Flags

| Flag | Description |
|------|-------------|
| `--deep-link-origin` | Signal that this session was launched from a deep link |
| `--deep-link-repo <slug>` | Repo slug the deep link `?repo=` parameter resolved to the current cwd |
| `--deep-link-last-fetch <ms>` | `FETCH_HEAD` mtime in epoch ms, precomputed by the deep link trampoline |

### Hooks / Init

| Flag | Description |
|------|-------------|
| `--init` | Run Setup hooks with init trigger, then continue |
| `--init-only` | Run Setup and SessionStart:startup hooks, then exit |
| `--maintenance` | Run Setup hooks with maintenance trigger, then continue |

### Teammate / Swarm Identity

These are set by the leader agent when spawning tmux teammates:

| Flag | Description |
|------|-------------|
| `--agent-id <id>` | Teammate agent ID |
| `--agent-name <name>` | Teammate display name |
| `--team-name <name>` | Team name for swarm coordination |
| `--agent-color <color>` | Teammate UI color |
| `--plan-mode-required` | Require plan mode before implementation |
| `--parent-session-id <id>` | Parent session ID for analytics correlation |
| `--teammate-mode <mode>` | How to spawn teammates: `auto`, `tmux`, or `in-process` |
| `--agent-type <type>` | Custom agent type for this teammate |

### Remote / Teleport

| Flag | Description |
|------|-------------|
| `--teleport [session]` | Resume a teleport session, optionally specify session ID |
| `--remote [description]` | Create a remote session with the given description |
| `--remote-control [name]` | Start an interactive session with Remote Control enabled (optionally named). Requires BRIDGE_MODE feature. |
| `--rc [name]` | Alias for `--remote-control`. Requires BRIDGE_MODE feature. |

### Advisor

| Flag | Description |
|------|-------------|
| `--advisor <model>` | Enable the server-side advisor tool with the specified model (alias or full ID). Only available when advisor configuration is permitted. |

### Feature-Gated Options

These options are only available when specific feature flags are enabled:

| Flag | Feature Gate | Description |
|------|-------------|-------------|
| `--proactive` | PROACTIVE / KAIROS | Start in proactive autonomous mode |
| `--messaging-socket-path <path>` | UDS_INBOX | Unix domain socket path for the UDS messaging server |
| `--brief` | KAIROS / KAIROS_BRIEF | Enable SendUserMessage tool for agent-to-user communication |
| `--assistant` | KAIROS | Force assistant mode (Agent SDK daemon use) |
| `--channels <servers...>` | KAIROS / KAIROS_CHANNELS | MCP servers whose channel notifications should register this session |
| `--dangerously-load-development-channels <servers...>` | KAIROS / KAIROS_CHANNELS | Load channel servers not on the approved allowlist (local dev only) |
| `--enable-auto-mode` | TRANSCRIPT_CLASSIFIER | Opt in to auto mode |
| `--hard-fail` | HARD_FAIL | Crash on logError calls instead of silently logging |

---

## Subcommands

### `claude mcp` — Configure and manage MCP servers

| Subcommand | Description |
|------------|-------------|
| `mcp serve` | Start the Claude Code MCP server |
| `mcp add` | Add an MCP server (interactive wizard) |
| `mcp add-json <name> <json>` | Add an MCP server with a JSON string |
| `mcp add-from-claude-desktop` | Import MCP servers from Claude Desktop (Mac and WSL only) |
| `mcp remove <name>` | Remove an MCP server |
| `mcp list` | List configured MCP servers |
| `mcp get <name>` | Get details about an MCP server |
| `mcp reset-project-choices` | Reset all approved/rejected project-scoped servers |

**`mcp serve` options:**
- `-d, --debug` — Enable debug mode
- `--verbose` — Override verbose mode setting from config

**`mcp remove` options:**
- `-s, --scope <scope>` — Configuration scope (local, user, or project)

**`mcp add-json` options:**
- `-s, --scope <scope>` — Configuration scope (default: `local`)
- `--client-secret` — Prompt for OAuth client secret (or set `MCP_CLIENT_SECRET` env var)

**`mcp add-from-claude-desktop` options:**
- `-s, --scope <scope>` — Configuration scope (default: `local`)

### `claude auth` — Manage authentication

| Subcommand | Description |
|------------|-------------|
| `auth login` | Sign in to your Anthropic account |
| `auth status` | Show authentication status |
| `auth logout` | Log out from your Anthropic account |

**`auth login` options:**
- `--email <email>` — Pre-populate email address on the login page
- `--sso` — Force SSO login flow
- `--console` — Use Anthropic Console (API usage billing) instead of Claude subscription
- `--claudeai` — Use Claude subscription (default)

**`auth status` options:**
- `--json` — Output as JSON (default)
- `--text` — Output as human-readable text

### `claude plugin` (alias: `plugins`) — Manage Claude Code plugins

| Subcommand | Description |
|------------|-------------|
| `plugin validate <path>` | Validate a plugin or marketplace manifest |
| `plugin list` | List installed plugins |
| `plugin install <plugin>` (alias: `i`) | Install a plugin from available marketplaces |
| `plugin uninstall <plugin>` (aliases: `remove`, `rm`) | Uninstall an installed plugin |
| `plugin enable <plugin>` | Enable a disabled plugin |
| `plugin disable [plugin]` | Disable an enabled plugin |
| `plugin update <plugin>` | Update a plugin to the latest version |
| `plugin marketplace add <source>` | Add a marketplace from a URL, path, or GitHub repo |
| `plugin marketplace list` | List all configured marketplaces |
| `plugin marketplace remove <name>` (alias: `rm`) | Remove a configured marketplace |
| `plugin marketplace update [name]` | Update marketplace(s) from their source |

**Common plugin options:**
- `-s, --scope <scope>` — Installation scope: user, project, or local
- `--cowork` — Use cowork_plugins directory (hidden)

**`plugin list` options:**
- `--json` — Output as JSON
- `--available` — Include available plugins from marketplaces (requires `--json`)

**`plugin uninstall` options:**
- `--keep-data` — Preserve the plugin's persistent data directory

**`plugin disable` options:**
- `-a, --all` — Disable all enabled plugins

**`plugin marketplace add` options:**
- `--sparse <paths...>` — Limit checkout to specific directories via git sparse-checkout (for monorepos)
- `--scope <scope>` — Where to declare the marketplace: user (default), project, or local

### `claude server` — Start a Claude Code session server

*(Feature-gated: DIRECT_CONNECT)*

| Option | Description | Default |
|--------|-------------|---------|
| `--port <number>` | HTTP port | `0` |
| `--host <string>` | Bind address | `0.0.0.0` |
| `--auth-token <token>` | Bearer token for auth | auto-generated |
| `--unix <path>` | Listen on a unix domain socket | — |
| `--workspace <dir>` | Default working directory for sessions | — |
| `--idle-timeout <ms>` | Idle timeout for detached sessions in ms (0 = never) | `600000` |
| `--max-sessions <n>` | Maximum concurrent sessions (0 = unlimited) | `32` |

### `claude ssh <host> [dir]` — Run Claude Code on a remote host

*(Feature-gated: SSH_REMOTE)*

| Option | Description |
|--------|-------------|
| `--permission-mode <mode>` | Permission mode for the remote session |
| `--dangerously-skip-permissions` | Skip all permission prompts on the remote |
| `--local` | e2e test mode — spawn the child CLI locally (skip ssh/deploy) |

### Other Subcommands

| Subcommand | Description |
|------------|-------------|
| `claude doctor` | Check the health of your Claude Code auto-updater |
| `claude update` (alias: `upgrade`) | Check for updates and install if available |
| `claude install [target]` | Install Claude Code native build (`stable`, `latest`, or specific version). Use `--force` to force install. |
| `claude setup-token` | Set up a long-lived authentication token (requires Claude subscription) |
| `claude agents` | List configured agents. Use `--setting-sources <sources>` to filter. |
| `claude open <cc-url>` | Connect to a Claude Code server (internal — use `cc://` URLs). Feature-gated: DIRECT_CONNECT. |
| `claude remote-control` (alias: `rc`) | Connect local environment for remote-control sessions via claude.ai/code. Feature-gated: BRIDGE_MODE. |
| `claude auto-mode defaults` | Print default auto mode rules as JSON. Feature-gated: TRANSCRIPT_CLASSIFIER. |
| `claude auto-mode config` | Print effective auto mode config. Feature-gated: TRANSCRIPT_CLASSIFIER. |
| `claude auto-mode critique` | Get AI feedback on custom auto mode rules (`--model <model>` to override model). Feature-gated: TRANSCRIPT_CLASSIFIER. |

---

## Examples

```bash
# Start interactive session
claude

# Non-interactive: pipe a prompt and get the response
claude -p "Explain this error"

# Continue the last conversation
claude --continue

# Resume a specific session
claude --resume abc123

# Use a specific model with high effort
claude --model opus --effort high

# Non-interactive with JSON streaming output
claude -p "Fix the bug" --output-format stream-json

# Set a budget limit
claude -p "Refactor the codebase" --max-budget-usd 5.00

# Use custom MCP servers
claude --mcp-config ./my-servers.json --strict-mcp-config

# Restrict available tools
claude --allowed-tools "Bash(git:*) Edit Read"

# Start in a new git worktree
claude -w my-feature

# Custom system prompt
claude --system-prompt "You are a security auditor" -p "Review this code"

# Add extra directories for tool access
claude --add-dir ../shared-lib --add-dir ../config

# Load plugins from a local directory
claude --plugin-dir ./my-plugins

# Define custom agents inline
claude --agents '{"reviewer": {"description": "Reviews code", "prompt": "You are a code reviewer"}}'

# Bare mode with explicit context
claude --bare --system-prompt "Fix bugs only" --mcp-config config.json -p "Fix the test"

# MCP server management
claude mcp add              # Interactive add
claude mcp list             # List all servers
claude mcp remove my-server # Remove a server

# Authentication
claude auth login --sso     # Login via SSO
claude auth status --text   # Check auth status

# Plugin management
claude plugin list --json
claude plugin install my-plugin -s project

# Check for updates
claude update
```
