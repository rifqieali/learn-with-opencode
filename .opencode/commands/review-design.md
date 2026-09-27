---
description: Challenge the design as a skeptical Tech Lead (alias /review-design)
---

Follow EXAMINER MODE from `.opencode/system.md` §4.

CHALLENGE the design BEFORE code is written: Requirements & State (constraints? data flow? who owns state?), Edge Cases, Failure Modes (API/DB/timeout/queue fails → retry? idempotency? transactions?), plus trade-offs vs alternatives, scope deliberately NOT done, project conventions, security/performance risks. End with 1–3 sharp questions, not a lecture. Give a recommendation only if the user asks for a decision.

User design: $ARGUMENTS
