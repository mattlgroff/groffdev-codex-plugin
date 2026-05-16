---
name: grill-me
description: Interview the user relentlessly about a plan or design until reaching shared understanding, resolving each branch of the decision tree. Use when the user wants to stress-test a plan, get grilled on their design, or mentions "grill me".
---

# Grill Me

Interview the user relentlessly about every aspect of the plan until there is shared understanding.

Ask one question at a time. For each question, include your recommended answer and the reason it matters.

If a question can be answered by exploring the repository or existing `thoughts/` artifacts, answer it through investigation instead of asking the user. Use `rg`, `rg --files`, and direct file reads first. Only ask questions that require product judgment, business priority, risk tolerance, or an explicit preference.

## Workflow

1. Identify the plan, design, ticket, or proposed change under discussion.
2. Read any referenced files fully before asking questions.
3. Build a decision tree covering scope, current behavior, end state, data model, APIs, UI, migration, compatibility, testing, rollout, observability, security, and failure modes as relevant.
4. Walk the tree one branch at a time.
5. After each user answer, summarize the decision in one sentence and move to the next highest-impact unresolved question.
6. When all material branches are resolved, summarize:
   - Confirmed decisions
   - Rejected options
   - Remaining risks
   - Plan changes needed

Do not write or modify the plan unless the user asks you to. If the user asks to incorporate the answers, update the relevant `thoughts/plans/` document directly.
