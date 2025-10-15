# Multi-Agent Orchestrator Change Log

> Keep this file current; it documents the evolution of the multi-agent design work. An outdated changelog breaks the orchestrator timeline.

## 2025-10-16
- Removed the inline `#agent` autocomplete experiment and reverted documentation to focus on the delegate picker and slash command flow.

## 2025-10-14
- Captured the baseline design artifacts (`AGENTS.md`, `config-design.md`, `instruction-design.md`, `persistence-design.md`, `error-handling.md`) compiled during the planning phase.
- Reiterated the requirement that this changelog must stay up to date as the multi-agent feature evolves.
- Scaffolded the `codex-multi-agent` crate with `AgentId`, `AgentRegistry`, and async config loading that merges global/agent/CLI overrides into an `AgentContext`.
- Wired the TUI bootstrapper to the new loader, introducing a `--agent` flag that scopes interactive runs to `~/.codex/agents/<agent_id>/`.
- Added `ai-temp/example-codex-home/` with ready-to-run config, instructions, and multiple agent directories for hands-on testing via `CODEX_HOME=...` and `--agent`.
- Authored `ai-temp/orchestration-integration.md`, outlining logic, UI/UX, and minimal-coupling hooks to let the primary agent delegate work to sub-agents in the existing codebase.
- Captured delegation decisions (single-flight execution, shared auth, primary-agent-composed prompts) inside `ai-temp/orchestration-integration.md`.
- Simplified the example Codex home to `ideas_provider` (gpt-5) and `critic` (gpt-5-nano) agents for easier manual testing.
- Delegated runs now stream live output (`DelegateEvent::Delta`) through the TUI, and remaining UX follow-ups are tracked in `ai-temp/ui-ux-delegation.md`.
- Added a dedicated status indicator while a delegate runs, restored the idle header on completion, and regression-tested streaming to prevent animation regressions.
- Updated the sample Codex home instructions/README, ensured the critic agent uses `gpt-5-nano`, and documented the new delegation UX in `ai-temp/ui-ux-delegation.md`.
- Documented plan-tool implementation patterns and how they inform future delegation tools (`ai-temp/tool-implementation-patterns.md`).
- Observed that the coordinator remains silent between delegate runs (e.g., between `#ideas_provider` completion and the `#critic` request) because tool composition happens model-side without emitting UI events; leaving this behaviour in place for now.
