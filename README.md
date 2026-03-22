# github-copilot-agent-orchestrators
agent orchestrators for various stacks, frameworks, and tasks

## Cost-aware orchestration policy

The orchestrators are configured to maximize quality per premium request:

- Main orchestrators use auto model selection for adaptive routing.
- Direct execution is preferred for clear, low-risk, narrow requests.
- Planner-first execution is required for ambiguous or high-risk work.
- Lightweight preflight triage is performed before escalating to Planner.

### Escalation gate

The orchestrator must call Planner when any of the following is true:

- Estimated scope exceeds 6 files and the task is not strictly additive in one bounded feature area.
- High-risk architecture changes are involved (for example: state management, core providers, routing/auth, shared cross-feature concerns, data/security changes).
- Requirements are ambiguous.

Exception:

- Purely mechanical, low-risk edits (rename-only, formatting-only, import cleanup) do not escalate based on file count alone.
