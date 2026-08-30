# AI Context: Master Entry Point

Welcome to the project context directory. This directory serves as the unified Single Source of Truth (SSoT) for all AI assistants.

> [!IMPORTANT]
> - Every new AI session must begin with [START_SESSION.md](START_SESSION.md).
> - Every AI session must end with [END_SESSION.md](END_SESSION.md).
> - No user prompt copy-pasting is required. The user initiates sessions simply by typing `start` and closes sessions by typing `end`.

---

## Mandatory Reading Sequence on Startup:
1. **[START_SESSION.md](START_SESSION.md)**: Auto-detects identity, runs `git pull --rebase`, and validates working copy.
2. **[PROJECT_OVERVIEW.md](PROJECT_OVERVIEW.md)**: Architecture map, tech stack, directory structure.
3. **[CURRENT_STATUS.md](CURRENT_STATUS.md)**: Current development phase, active features, verified vs unverified items.
4. **[TODO.md](TODO.md)**: Prioritized task list.
5. **[DECISIONS.md](DECISIONS.md)**: Permanent constitutional project rules and architecture decisions.
6. **`AI_CONTEXT/SESSIONS/[Your AI Identity].md`**: Your designated session history and last known state.
7. **[SESSIONS/REGISTRY.md](SESSIONS/REGISTRY.md)**: Central active multi-AI roster and heartbeat coordination.
