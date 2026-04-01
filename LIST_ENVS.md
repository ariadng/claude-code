# Claude Code Environment Variables Reference

Complete reference for all environment variables recognized by Claude Code.

---

## Authentication & API

### API Keys & Tokens

| Variable | Description |
|----------|-------------|
| `ANTHROPIC_API_KEY` | Anthropic API key for direct API access |
| `ANTHROPIC_AUTH_TOKEN` | Anthropic auth token (alternative to API key) |
| `CLAUDE_CODE_OAUTH_TOKEN` | OAuth token for Claude Code authentication |
| `CLAUDE_CODE_OAUTH_REFRESH_TOKEN` | OAuth refresh token |
| `CLAUDE_CODE_OAUTH_TOKEN_FILE_DESCRIPTOR` | File descriptor to read OAuth token from |
| `CLAUDE_CODE_API_KEY_FILE_DESCRIPTOR` | File descriptor to read API key from |
| `CLAUDE_CODE_API_KEY_HELPER_TTL_MS` | TTL in milliseconds for API key helper cache |
| `CLAUDE_CODE_SESSION_ACCESS_TOKEN` | Session-specific access token |
| `CLAUDE_CODE_WEBSOCKET_AUTH_FILE_DESCRIPTOR` | File descriptor for WebSocket auth credentials |
| `AWS_BEARER_TOKEN_BEDROCK` | AWS bearer token for Bedrock authentication |
| `ANTHROPIC_FOUNDRY_API_KEY` | API key for Anthropic Foundry |

### OAuth Configuration

| Variable | Description |
|----------|-------------|
| `CLAUDE_CODE_OAUTH_CLIENT_ID` | OAuth client ID |
| `CLAUDE_CODE_OAUTH_SCOPES` | OAuth scopes to request |
| `CLAUDE_CODE_CUSTOM_OAUTH_URL` | Custom OAuth URL |

---

## Provider Selection

| Variable | Description |
|----------|-------------|
| `CLAUDE_CODE_USE_BEDROCK` | Use Amazon Bedrock as the API provider (truthy) |
| `CLAUDE_CODE_USE_VERTEX` | Use Google Vertex AI as the API provider (truthy) |
| `CLAUDE_CODE_USE_FOUNDRY` | Use Anthropic Foundry as the API provider (truthy) |
| `CLAUDE_CODE_SKIP_BEDROCK_AUTH` | Skip Bedrock authentication (for custom auth setups) |
| `CLAUDE_CODE_SKIP_VERTEX_AUTH` | Skip Vertex AI authentication |
| `CLAUDE_CODE_SKIP_FOUNDRY_AUTH` | Skip Foundry authentication |
| `CLAUDE_CODE_PROVIDER_MANAGED_BY_HOST` | Signal that the host application manages provider routing. Prevents user settings from overriding provider config. |

---

## API Endpoints & Base URLs

| Variable | Description |
|----------|-------------|
| `ANTHROPIC_BASE_URL` | Base URL for the Anthropic API |
| `ANTHROPIC_BEDROCK_BASE_URL` | Base URL for the Amazon Bedrock endpoint |
| `ANTHROPIC_UNIX_SOCKET` | Unix socket path for API communication (used by `claude ssh` for auth tunneling) |

---

## Model Configuration

### Default Model Selection

| Variable | Description |
|----------|-------------|
| `ANTHROPIC_MODEL` | Override the default model for the session |
| `CLAUDE_CODE_SUBAGENT_MODEL` | Model to use for subagent/agent tool calls |
| `ANTHROPIC_SMALL_FAST_MODEL` | Override the small/fast model (Haiku equivalent) |
| `ANTHROPIC_SMALL_FAST_MODEL_AWS_REGION` | AWS region for the small/fast model |

### Custom Model Defaults

| Variable | Description |
|----------|-------------|
| `ANTHROPIC_DEFAULT_SONNET_MODEL` | Custom model ID for the "Sonnet" option |
| `ANTHROPIC_DEFAULT_SONNET_MODEL_NAME` | Display name for the custom Sonnet model |
| `ANTHROPIC_DEFAULT_SONNET_MODEL_DESCRIPTION` | Description for the custom Sonnet model |
| `ANTHROPIC_DEFAULT_OPUS_MODEL` | Custom model ID for the "Opus" option |
| `ANTHROPIC_DEFAULT_OPUS_MODEL_NAME` | Display name for the custom Opus model |
| `ANTHROPIC_DEFAULT_OPUS_MODEL_DESCRIPTION` | Description for the custom Opus model |
| `ANTHROPIC_DEFAULT_HAIKU_MODEL` | Custom model ID for the "Haiku" option |
| `ANTHROPIC_DEFAULT_HAIKU_MODEL_NAME` | Display name for the custom Haiku model |
| `ANTHROPIC_DEFAULT_HAIKU_MODEL_DESCRIPTION` | Description for the custom Haiku model |

### Custom Model Option

| Variable | Description |
|----------|-------------|
| `ANTHROPIC_CUSTOM_MODEL_OPTION` | Add a fully custom model ID to the model picker |
| `ANTHROPIC_CUSTOM_MODEL_OPTION_NAME` | Display name for the custom model option |
| `ANTHROPIC_CUSTOM_MODEL_OPTION_DESCRIPTION` | Description for the custom model option |

### Vertex AI Region Overrides

| Variable | Description |
|----------|-------------|
| `CLOUD_ML_REGION` | Default Vertex AI region (default: `us-east5`) |
| `VERTEX_REGION_CLAUDE_HAIKU_4_5` | Vertex region for Claude Haiku 4.5 |
| `VERTEX_REGION_CLAUDE_3_5_HAIKU` | Vertex region for Claude 3.5 Haiku |
| `VERTEX_REGION_CLAUDE_3_5_SONNET` | Vertex region for Claude 3.5 Sonnet |
| `VERTEX_REGION_CLAUDE_3_7_SONNET` | Vertex region for Claude 3.7 Sonnet |
| `VERTEX_REGION_CLAUDE_4_0_OPUS` | Vertex region for Claude Opus 4 |
| `VERTEX_REGION_CLAUDE_4_0_SONNET` | Vertex region for Claude Sonnet 4 |
| `VERTEX_REGION_CLAUDE_4_1_OPUS` | Vertex region for Claude Opus 4.1 |
| `VERTEX_REGION_CLAUDE_4_5_SONNET` | Vertex region for Claude Sonnet 4.5 |
| `VERTEX_REGION_CLAUDE_4_6_SONNET` | Vertex region for Claude Sonnet 4.6 |
| `ANTHROPIC_VERTEX_PROJECT_ID` | Google Cloud project ID for Vertex AI |

### AWS Region

| Variable | Description |
|----------|-------------|
| `AWS_REGION` | AWS region (used for Bedrock) |
| `AWS_DEFAULT_REGION` | Fallback AWS region (default: `us-east-1`) |

---

## API Behavior

| Variable | Description |
|----------|-------------|
| `ANTHROPIC_BETAS` | Beta headers to include in API requests |
| `ANTHROPIC_CUSTOM_HEADERS` | Custom headers to include in API requests |
| `CLAUDE_CODE_MAX_OUTPUT_TOKENS` | Maximum output tokens for API responses |
| `MAX_THINKING_TOKENS` | Maximum number of thinking tokens |
| `CLAUDE_CODE_MAX_CONTEXT_TOKENS` | Maximum context window tokens |
| `CLAUDE_CODE_MAX_RETRIES` | Maximum number of API retries |
| `CLAUDE_CODE_EXTRA_BODY` | Extra JSON body parameters for API requests |
| `CLAUDE_CODE_EXTRA_METADATA` | Extra metadata to include in API requests |
| `CLAUDE_CODE_DISABLE_EXPERIMENTAL_BETAS` | Disable experimental beta features in API calls |
| `CLAUDE_CODE_DISABLE_NONSTREAMING_FALLBACK` | Disable fallback to non-streaming API calls |
| `CLAUDE_CODE_DISABLE_ADAPTIVE_THINKING` | Disable adaptive thinking |
| `CLAUDE_CODE_DISABLE_THINKING` | Disable thinking entirely |
| `CLAUDE_CODE_STALL_TIMEOUT_MS_FOR_TESTING` | Override stream stall timeout (for testing) |
| `CLAUDE_STREAM_IDLE_TIMEOUT_MS` | Idle timeout for streaming connections |
| `CLAUDE_ENABLE_STREAM_WATCHDOG` | Enable stream watchdog for detecting stalled streams |
| `DISABLE_PROMPT_CACHING` | Disable prompt caching globally |
| `DISABLE_PROMPT_CACHING_SONNET` | Disable prompt caching for Sonnet models |
| `DISABLE_PROMPT_CACHING_OPUS` | Disable prompt caching for Opus models |
| `DISABLE_PROMPT_CACHING_HAIKU` | Disable prompt caching for Haiku models |
| `ENABLE_PROMPT_CACHING_1H_BEDROCK` | Enable 1-hour prompt caching on Bedrock |
| `DISABLE_INTERLEAVED_THINKING` | Disable interleaved thinking mode |
| `CLAUDE_CODE_ATTRIBUTION_HEADER` | Custom attribution header value |

---

## Tool Configuration

### Bash Tool

| Variable | Description |
|----------|-------------|
| `BASH_MAX_OUTPUT_LENGTH` | Maximum output length for Bash tool results |
| `BASH_DEFAULT_TIMEOUT_MS` | Default timeout for Bash commands in milliseconds |
| `BASH_MAX_TIMEOUT_MS` | Maximum allowed timeout for Bash commands |
| `CLAUDE_BASH_MAINTAIN_PROJECT_WORKING_DIR` | Reset working directory to project root after each Bash command |
| `CLAUDE_CODE_DISABLE_COMMAND_INJECTION_CHECK` | Disable command injection security checks |

### MCP (Model Context Protocol)

| Variable | Description |
|----------|-------------|
| `MCP_TIMEOUT` | Connection timeout for MCP servers in milliseconds (default: 30000) |
| `MCP_TOOL_TIMEOUT` | Execution timeout for individual MCP tool calls |
| `MAX_MCP_OUTPUT_TOKENS` | Maximum output tokens from MCP tool results |
| `MCP_CLIENT_SECRET` | OAuth client secret for MCP server auth |
| `MCP_OAUTH_CALLBACK_PORT` | Port for MCP OAuth callback |
| `MCP_SERVER_CONNECTION_BATCH_SIZE` | Number of MCP servers to connect concurrently |
| `MCP_REMOTE_SERVER_CONNECTION_BATCH_SIZE` | Number of remote MCP servers to connect concurrently |
| `ENABLE_MCP_LARGE_OUTPUT_FILES` | Enable large output file support for MCP |
| `CLAUDE_CODE_MCP_INSTR_DELTA` | MCP instrumentation delta |

### File & Search Tools

| Variable | Description |
|----------|-------------|
| `CLAUDE_CODE_FILE_READ_MAX_OUTPUT_TOKENS` | Maximum output tokens for file read operations |
| `CLAUDE_CODE_GLOB_TIMEOUT_SECONDS` | Timeout in seconds for glob file searches |
| `CLAUDE_CODE_GLOB_HIDDEN` | Include hidden files in glob searches |
| `CLAUDE_CODE_GLOB_NO_IGNORE` | Don't respect .gitignore in glob searches |
| `CLAUDE_CODE_USE_NATIVE_FILE_SEARCH` | Use native file search implementation |
| `USE_BUILTIN_RIPGREP` | Use the built-in ripgrep binary instead of system ripgrep |
| `CLAUDE_CODE_MAX_TOOL_USE_CONCURRENCY` | Maximum concurrent tool executions |

---

## Session & Configuration

### Paths & Directories

| Variable | Description |
|----------|-------------|
| `CLAUDE_CONFIG_DIR` | Override the Claude config directory (default: `~/.claude`) |
| `CLAUDE_CODE_TMPDIR` | Override the temp directory for Claude Code |
| `CLAUDE_CODE_DEBUG_LOGS_DIR` | Directory for debug log files |
| `CLAUDE_CODE_DIAGNOSTICS_FILE` | Path for diagnostics output file |
| `CLAUDE_CODE_MANAGED_SETTINGS_PATH` | Path to managed settings file |
| `CLAUDE_CODE_PLUGIN_CACHE_DIR` | Directory for plugin cache |
| `CLAUDE_CODE_PLUGIN_SEED_DIR` | Seed directory for plugins |

### Session Identity

| Variable | Description |
|----------|-------------|
| `CLAUDE_CODE_SESSION_ID` | Override the session ID |
| `CLAUDE_CODE_SESSION_NAME` | Set a display name for the session |
| `CLAUDE_CODE_SESSION_KIND` | Session kind identifier |
| `CLAUDE_CODE_ENTRYPOINT` | How Claude Code was launched: `cli`, `sdk-ts`, `sdk-py`, `sdk-cli`, `claude-desktop`, `local-agent` |
| `CLAUDE_CODE_TAGS` | Tags for the current session |

### Account & Organization

| Variable | Description |
|----------|-------------|
| `CLAUDE_CODE_ACCOUNT_UUID` | Account UUID for the current user |
| `CLAUDE_CODE_ACCOUNT_TAGGED_ID` | Tagged account ID |
| `CLAUDE_CODE_ORGANIZATION_UUID` | Organization UUID |
| `CLAUDE_CODE_USER_EMAIL` | User email address |

---

## Shell & Environment

| Variable | Description |
|----------|-------------|
| `CLAUDE_CODE_SHELL` | Override the shell used for Bash tool commands |
| `CLAUDE_CODE_SHELL_PREFIX` | Prefix command for shell execution (e.g., for MCP server commands) |
| `CLAUDE_CODE_GIT_BASH_PATH` | Path to Git Bash on Windows |
| `CLAUDE_CODE_HOST_PLATFORM` | Override the detected host platform |
| `CLAUDE_CODE_ENVIRONMENT_KIND` | Environment kind identifier |
| `CLAUDE_CODE_CONTAINER_ID` | Container ID when running in a container |
| `CLAUDE_ENV_FILE` | Path to an environment file to load |

---

## Behavioral Toggles

### Feature Enables

| Variable | Description |
|----------|-------------|
| `CLAUDE_CODE_ENABLE_TELEMETRY` | Enable OpenTelemetry telemetry export |
| `CLAUDE_CODE_ENABLE_CFC` | Enable CFC (context file checkpointing) |
| `CLAUDE_CODE_ENABLE_SDK_FILE_CHECKPOINTING` | Enable file checkpointing for SDK mode |
| `CLAUDE_CODE_ENABLE_TASKS` | Enable tasks feature |
| `CLAUDE_CODE_ENABLE_PROMPT_SUGGESTION` | Enable prompt suggestions |
| `CLAUDE_CODE_ENABLE_TOKEN_USAGE_ATTACHMENT` | Enable token usage attachment in responses |
| `CLAUDE_CODE_ENABLE_FINE_GRAINED_TOOL_STREAMING` | Enable fine-grained tool streaming |
| `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS` | Enable experimental agent teams/swarm feature |
| `CLAUDE_CODE_ALWAYS_ENABLE_EFFORT` | Always enable effort level control |
| `ENABLE_TOOL_SEARCH` | Enable tool search functionality |
| `ENABLE_SESSION_PERSISTENCE` | Enable session persistence |
| `ENABLE_LSP_TOOL` | Enable LSP (Language Server Protocol) tool |
| `ENABLE_LOCKLESS_UPDATES` | Enable lockless auto-updates |

### Feature Disables

| Variable | Description |
|----------|-------------|
| `CLAUDE_CODE_SIMPLE` | Minimal/bare mode — skip hooks, LSP, plugins, auto-memory, CLAUDE.md discovery (equivalent to `--bare`) |
| `CLAUDE_CODE_DISABLE_AUTO_MEMORY` | Disable automatic memory/CLAUDE.md updates |
| `CLAUDE_CODE_DISABLE_CLAUDE_MDS` | Disable CLAUDE.md file loading |
| `CLAUDE_CODE_DISABLE_GIT_INSTRUCTIONS` | Disable automatic git instructions in system prompt |
| `CLAUDE_CODE_DISABLE_TERMINAL_TITLE` | Disable setting the terminal title to "claude" |
| `CLAUDE_CODE_DISABLE_MOUSE` | Disable all mouse support |
| `CLAUDE_CODE_DISABLE_MOUSE_CLICKS` | Disable mouse click support only |
| `CLAUDE_CODE_DISABLE_BACKGROUND_TASKS` | Disable background tasks |
| `CLAUDE_CODE_DISABLE_FILE_CHECKPOINTING` | Disable file checkpointing |
| `CLAUDE_CODE_DISABLE_FAST_MODE` | Disable fast mode |
| `CLAUDE_CODE_DISABLE_1M_CONTEXT` | Disable 1M context window |
| `CLAUDE_CODE_DISABLE_ATTACHMENTS` | Disable file attachments |
| `CLAUDE_CODE_DISABLE_CRON` | Disable cron/scheduled tasks |
| `CLAUDE_CODE_DISABLE_POLICY_SKILLS` | Disable policy-based skills |
| `CLAUDE_CODE_DISABLE_LEGACY_MODEL_REMAP` | Disable legacy model name remapping |
| `CLAUDE_CODE_DISABLE_PRECOMPACT_SKIP` | Disable pre-compact skip optimization |
| `CLAUDE_CODE_DISABLE_ADVISOR_TOOL` | Disable the advisor tool |
| `CLAUDE_CODE_DISABLE_OFFICIAL_MARKETPLACE_AUTOINSTALL` | Disable auto-install of official marketplace plugins |
| `DISABLE_AUTO_COMPACT` | Disable automatic context compaction |
| `DISABLE_COMPACT` | Disable compaction entirely |
| `DISABLE_COST_WARNINGS` | Disable cost warning notifications |
| `DISABLE_TELEMETRY` | Disable all telemetry |
| `DISABLE_ERROR_REPORTING` | Disable error reporting |
| `DISABLE_AUTOUPDATER` | Disable the auto-updater |

### Command Disables

| Variable | Description |
|----------|-------------|
| `DISABLE_LOGIN_COMMAND` | Disable the `/login` command |
| `DISABLE_LOGOUT_COMMAND` | Disable the `/logout` command |
| `DISABLE_UPGRADE_COMMAND` | Disable the `/upgrade` command |
| `DISABLE_FEEDBACK_COMMAND` | Disable the `/feedback` command |
| `DISABLE_EXTRA_USAGE_COMMAND` | Disable the `/extra-usage` command |
| `DISABLE_BUG_COMMAND` | Disable the `/bug` command |
| `DISABLE_DOCTOR_COMMAND` | Disable the `/doctor` command |
| `DISABLE_INSTALL_GITHUB_APP_COMMAND` | Disable the `/install-github-app` command |
| `DISABLE_INSTALLATION_CHECKS` | Disable installation health checks |

---

## Debugging & Diagnostics

| Variable | Description |
|----------|-------------|
| `CLAUDE_DEBUG` | Enable debug mode |
| `CLAUDE_CODE_DEBUG_LOG_LEVEL` | Debug log level |
| `CLAUDE_CODE_DEBUG_REPAINTS` | Debug UI repaints |
| `CLAUDE_CODE_PROFILE_STARTUP` | Enable startup profiling |
| `CLAUDE_CODE_PROFILE_QUERY` | Enable query profiling |
| `CLAUDE_CODE_PERFETTO_TRACE` | Enable Perfetto trace output |
| `CLAUDE_CODE_PERFETTO_WRITE_INTERVAL_S` | Perfetto write interval in seconds |
| `CLAUDE_CODE_SESSION_LOG` | Path for session log output |
| `CLAUDE_CODE_JSONL_TRANSCRIPT` | Path for JSONL transcript output |
| `CLAUDE_CODE_COMMIT_LOG` | Enable commit logging |
| `CLAUDE_CODE_EAGER_FLUSH` | Force eager flushing of output |
| `CLAUDE_CODE_NO_FLICKER` | Disable UI flicker (buffering optimization) |
| `CLAUDE_CODE_TERMINAL_RECORDING` | Enable terminal recording |
| `CLAUDE_CODE_EXIT_AFTER_FIRST_RENDER` | Exit after first render (for testing) |
| `CLAUDE_CODE_EXIT_AFTER_STOP_DELAY` | Delay before exit after stop (for testing) |
| `DEBUG` | General debug flag (Node.js convention) |

---

## Proxy & Network

| Variable | Description |
|----------|-------------|
| `HTTP_PROXY` | HTTP proxy URL |
| `HTTPS_PROXY` | HTTPS proxy URL |
| `NO_PROXY` | Comma-separated list of hosts to bypass proxy |
| `CLAUDE_CODE_PROXY_RESOLVES_HOSTS` | Indicate that the proxy handles DNS resolution |
| `NODE_EXTRA_CA_CERTS` | Path to additional CA certificates |
| `SSL_CERT_FILE` | Path to SSL certificate file |
| `CLAUDE_CODE_CLIENT_CERT` | Path to client certificate for mTLS |
| `CLAUDE_CODE_CLIENT_KEY` | Path to client key for mTLS |
| `CLAUDE_CODE_CLIENT_KEY_PASSPHRASE` | Passphrase for the client key |

---

## OpenTelemetry

| Variable | Description |
|----------|-------------|
| `OTEL_EXPORTER_OTLP_ENDPOINT` | OTLP exporter endpoint URL |
| `OTEL_EXPORTER_OTLP_HEADERS` | Headers for OTLP exporter |
| `OTEL_EXPORTER_OTLP_PROTOCOL` | Protocol for OTLP exporter (`grpc`, `http/protobuf`, `http/json`) |
| `OTEL_METRICS_EXPORTER` | Metrics exporter type |
| `OTEL_METRIC_EXPORT_INTERVAL` | Metrics export interval |
| `OTEL_TRACES_EXPORTER` | Traces exporter type |
| `OTEL_TRACES_EXPORT_INTERVAL` | Traces export interval |
| `OTEL_LOGS_EXPORTER` | Logs exporter type |
| `OTEL_LOGS_EXPORT_INTERVAL` | Logs export interval |
| `OTEL_EXPORTER_OTLP_LOGS_PROTOCOL` | Protocol for OTLP logs exporter |
| `OTEL_EXPORTER_OTLP_METRICS_PROTOCOL` | Protocol for OTLP metrics exporter |
| `OTEL_EXPORTER_OTLP_TRACES_PROTOCOL` | Protocol for OTLP traces exporter |
| `OTEL_LOG_TOOL_CONTENT` | Include tool content in telemetry logs |
| `OTEL_LOG_TOOL_DETAILS` | Include tool details in telemetry logs |
| `OTEL_LOG_USER_PROMPTS` | Include user prompts in telemetry logs |
| `CLAUDE_CODE_OTEL_FLUSH_TIMEOUT_MS` | Timeout for OTLP flush operations |
| `CLAUDE_CODE_OTEL_SHUTDOWN_TIMEOUT_MS` | Timeout for OTLP shutdown |
| `CLAUDE_CODE_OTEL_HEADERS_HELPER_DEBOUNCE_MS` | Debounce interval for OTLP headers helper |
| `CLAUDE_CODE_ENHANCED_TELEMETRY_BETA` | Enable enhanced telemetry beta features |

---

## Compaction & Context Management

| Variable | Description |
|----------|-------------|
| `CLAUDE_CODE_AUTO_COMPACT_WINDOW` | Context percentage threshold that triggers auto-compaction |
| `CLAUDE_CODE_AUTOCOMPACT_PCT_OVERRIDE` | Override the auto-compact percentage threshold |
| `CLAUDE_AFTER_LAST_COMPACT` | Instructions to prepend after compaction |
| `CLAUDE_CODE_STREAMLINED_OUTPUT` | Enable streamlined output mode |

---

## Remote & Bridge

| Variable | Description |
|----------|-------------|
| `CLAUDE_CODE_REMOTE` | Signal that Claude Code is running in a remote environment |
| `CLAUDE_CODE_REMOTE_SESSION_ID` | Remote session ID |
| `CLAUDE_CODE_REMOTE_ENVIRONMENT_TYPE` | Type of remote environment |
| `CLAUDE_CODE_REMOTE_MEMORY_DIR` | Directory for remote memory storage |
| `CLAUDE_CODE_REMOTE_SEND_KEEPALIVES` | Send keepalive signals in remote mode |
| `CLAUDE_CODE_SSE_PORT` | SSE (Server-Sent Events) port for remote connections |
| `CLAUDE_BRIDGE_BASE_URL` | Base URL for bridge connections |
| `CLAUDE_BRIDGE_OAUTH_TOKEN` | OAuth token for bridge authentication |
| `CLAUDE_BRIDGE_SESSION_INGRESS_URL` | Session ingress URL for bridge |
| `CLAUDE_CODE_USE_CCR_V2` | Use CCR v2 protocol |
| `CLAUDE_BRIDGE_USE_CCR_V2` | Use CCR v2 for bridge connections |

---

## IDE Integration

| Variable | Description |
|----------|-------------|
| `CLAUDE_CODE_IDE_HOST_OVERRIDE` | Override IDE host detection |
| `CLAUDE_CODE_IDE_SKIP_AUTO_INSTALL` | Skip automatic IDE extension installation |
| `CLAUDE_CODE_IDE_SKIP_VALID_CHECK` | Skip IDE validation checks |

---

## Agent SDK

| Variable | Description |
|----------|-------------|
| `CLAUDE_AGENT_SDK_CLIENT_APP` | Client application name for Agent SDK |
| `CLAUDE_AGENT_SDK_VERSION` | Agent SDK version |
| `CLAUDE_AGENT_SDK_DISABLE_BUILTIN_AGENTS` | Disable built-in agents in SDK mode |
| `CLAUDE_AGENT_SDK_MCP_NO_PREFIX` | Don't prefix MCP tool names in SDK mode |
| `CLAUDE_CODE_EMIT_SESSION_STATE_EVENTS` | Emit session state events for SDK consumers |
| `CLAUDE_CODE_EMIT_TOOL_USE_SUMMARIES` | Emit tool use summaries for SDK consumers |
| `CLAUDE_CODE_RESUME_INTERRUPTED_TURN` | Resume an interrupted turn in SDK mode |

---

## Plugin System

| Variable | Description |
|----------|-------------|
| `CLAUDE_CODE_PLUGIN_CACHE_DIR` | Override plugin cache directory |
| `CLAUDE_CODE_PLUGIN_SEED_DIR` | Plugin seed directory for initial plugins |
| `CLAUDE_CODE_PLUGIN_GIT_TIMEOUT_MS` | Git timeout for plugin operations in milliseconds |
| `CLAUDE_CODE_PLUGIN_USE_ZIP_CACHE` | Use zip-based caching for plugins |
| `CLAUDE_CODE_SYNC_PLUGIN_INSTALL` | Synchronously install plugins |
| `CLAUDE_CODE_SYNC_PLUGIN_INSTALL_TIMEOUT_MS` | Timeout for synchronous plugin install |
| `CLAUDE_CODE_USE_COWORK_PLUGINS` | Use cowork plugins directory |
| `FORCE_AUTOUPDATE_PLUGINS` | Force auto-update of plugins |

---

## Sandbox & Security

| Variable | Description |
|----------|-------------|
| `CLAUDE_CODE_BUBBLEWRAP` | Enable Bubblewrap sandboxing |
| `CLAUDE_CODE_ADDITIONAL_PROTECTION` | Enable additional security protections |
| `IS_SANDBOX` | Signal that Claude Code is running in a sandbox |

---

## Miscellaneous

| Variable | Description |
|----------|-------------|
| `CLAUDE_CODE_EFFORT_LEVEL` | Default effort level (`low`, `medium`, `high`, `max`) |
| `CLAUDE_CODE_AGENT` | Default agent for sessions |
| `CLAUDE_CODE_SYNTAX_HIGHLIGHT` | Enable/disable syntax highlighting |
| `CLAUDE_CODE_TMUX_TRUECOLOR` | Enable truecolor support in tmux |
| `CLAUDE_CODE_SKIP_PROMPT_HISTORY` | Skip prompt history saving |
| `CLAUDE_CODE_DONT_INHERIT_ENV` | Don't inherit environment variables in subprocesses |
| `CLAUDE_CODE_SUBPROCESS_ENV_SCRUB` | Scrub environment variables in subprocesses |
| `CLAUDE_CODE_NEW_INIT` | Use new init flow |
| `CLAUDE_CODE_REPL` | Signal that Claude Code is running in REPL mode |
| `CLAUDE_CODE_WORKER_EPOCH` | Worker epoch identifier |
| `CLAUDE_CODE_ACTION` | Current action being performed |
| `CLAUDE_CODE_BASE_REF` | Base git ref for comparisons |
| `CLAUDE_CODE_VERIFY_PLAN` | Verify plan before execution |
| `CLAUDE_CODE_PLAN_MODE_REQUIRED` | Require plan mode before implementation |
| `CLAUDE_CODE_PLAN_MODE_INTERVIEW_PHASE` | Start plan mode in interview phase |
| `CLAUDE_CODE_COORDINATOR_MODE` | Enable coordinator mode |
| `CLAUDE_CODE_BRIEF` | Enable brief mode |
| `CLAUDE_CODE_PROACTIVE` | Enable proactive mode |
| `CLAUDE_CODE_UNDERCOVER` | Enable undercover mode |
| `CLAUDE_CODE_IS_COWORK` | Signal that Claude Code is running as a coworker |
| `CLAUDE_CODE_COWORKER_TYPE` | Type of coworker |
| `CLAUDE_CODE_MESSAGING_SOCKET` | Path to messaging socket |
| `CLAUDE_CODE_TASK_LIST_ID` | Task list ID for task management |
| `CLAUDE_CODE_CHROME_PERMISSION_MODE` | Permission mode for Chrome integration |
| `CLAUDE_CODE_BLOCKING_LIMIT_OVERRIDE` | Override blocking rate limit |
| `CLAUDE_CODE_UNATTENDED_RETRY` | Enable unattended retry behavior |
| `CLAUDE_CODE_WORKSPACE_HOST_PATHS` | Host paths for workspace access |
| `CLAUDE_CODE_SAVE_HOOK_ADDITIONAL_CONTEXT` | Save additional context in hook events |
| `CLAUDE_CODE_SESSIONEND_HOOKS_TIMEOUT_MS` | Timeout for session end hooks |
| `CLAUDE_CODE_SLOW_OPERATION_THRESHOLD_MS` | Threshold for logging slow operations |
| `CLAUDE_CODE_ADDITIONAL_DIRECTORIES_CLAUDE_MD` | Additional directories to search for CLAUDE.md files |
| `CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC` | Disable non-essential network traffic |
| `CLAUDE_CODE_GB_BASE_URL` | GrowthBook base URL override |
| `CLAUDE_CODE_DATADOG_FLUSH_INTERVAL_MS` | Datadog flush interval |
| `SCROLLBACK_BYTES` | Terminal scrollback buffer size in bytes |
| `EDITOR` | Preferred text editor |
| `VISUAL` | Preferred visual editor |
| `BROWSER` | Preferred browser |
| `CI` | Signal that Claude Code is running in a CI environment |
| `NODE_ENV` | Node.js environment (`test`, `development`, `production`) |

---

## Summary by Prefix

| Prefix | Count | Purpose |
|--------|-------|---------|
| `ANTHROPIC_*` | ~20 | API keys, base URLs, model defaults, provider config |
| `CLAUDE_CODE_*` | ~130 | Core Claude Code configuration, features, behavior |
| `CLAUDE_*` (other) | ~15 | Config dir, debug, bridge, bash, agent SDK |
| `OTEL_*` | ~20 | OpenTelemetry telemetry configuration |
| `DISABLE_*` | ~15 | Feature and command disable switches |
| `ENABLE_*` | ~10 | Feature enable switches |
| `VERTEX_REGION_*` | ~10 | Vertex AI per-model region overrides |
| `AWS_*` | ~5 | AWS/Bedrock region and auth |
| `MCP_*` | ~7 | MCP server configuration |
| `BASH_*` | ~3 | Bash tool configuration |
