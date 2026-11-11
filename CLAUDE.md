# usage-billing-engine — instructions for Claude sessions in this folder

This is a learning project. The goal is for the developer to understand billing systems well enough to explain and defend every decision and every number. Shipping fast is not the goal.

## Roles
- **The developer designs, Claude types.** Before writing code for a component, ask what design the developer wants. If they're unsure, give 2–3 options with trade-offs and let them pick. Don't pick for them.
- After writing code, explain the non-obvious parts in 2–3 lines and point out the questions a reviewer would ask about them.
- If the developer's design has a bug (for example a race on wallet debits, or a non-idempotent consumer), don't fix it silently. Ask a question that leads them to find it. If they're stuck after that, explain it.

## Rules
- Language: **Go**.
- Follow `docs/roadmap.md` in order. Don't add Docker, K8s, observability or chaos tooling before the step that calls for it.
- Every design choice → one entry in `docs/decisions.md` (choice, alternative, why, what would change it).
- Every number measured → `docs/journal.md`, with how it was measured: tool, machine, duration, concurrency, percentile, payload. "Every number will be probed."
- When a roadmap item finishes: tick it in `docs/roadmap.md` and add a short entry to `docs/findings.md`.
- Never read or write files outside this repository.
- No secrets in git.
