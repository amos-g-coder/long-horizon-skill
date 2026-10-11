---
name: long-horizon
description: Optimize and immediately execute ambitious Codex Goal-mode requests that may span many milestones or context cycles. Use when the user explicitly invokes `$long-horizon` or asks Codex to autonomously carry a multi-day objective to completion; do not use for ordinary one-turn work or planning-only requests.
---

# Long Horizon

Turn the user's request into a lean execution contract for the current Codex harness, then act on it immediately. Do not end the turn after proposing an optimized prompt, ask for a second “proceed,” or silently broaden the assignment.

## Preserve the real objective

Treat the user's request, referenced artifacts, existing repository instructions, and active Goal-mode objective as authoritative. Preserve explicit deliverables, technologies, quality bars, exclusions, deadlines, budgets, and approval boundaries.

Fill gaps only when doing so is necessary to execute:

- Resolve facts from the workspace or authoritative sources before inferring them.
- Prefer reversible defaults supported by project conventions.
- Record material assumptions and how they will be validated.
- Never invent credentials, external facts, user preferences, business rules, success metrics, or permission for side effects.
- Ask only when an unresolved choice would materially change the outcome and no safe, reversible default exists. A question is for missing direction, not permission to begin ordinary in-scope work.

When an active goal already exists, align work to it; do not create a duplicate goal. Keep working across continuations until the completion contract is satisfied or a genuine stop condition trips.

## Compile the execution contract

Start with the smallest useful reconnaissance: read applicable instructions, inspect current state and relevant artifacts, and identify available verification. Do not front-load the whole repository or research tangential possibilities.

Compile a compact working contract containing only decision-relevant content:

1. **Outcome** — the user-visible end state.
2. **Deliverables** — concrete artifacts or changes that must exist.
3. **Definition of done** — observable acceptance criteria and required evidence.
4. **Scope** — included work, non-goals, and preserved behavior.
5. **Constraints** — technical, safety, privacy, cost, time, and compatibility requirements.
6. **Authority** — allowed local actions and actions that require approval.
7. **Milestones** — dependency-aware checkpoints, each with its own validation.
8. **Assumptions and risks** — only material uncertainties, detection signals, and fallbacks.
9. **Stop policy** — completion, retry, circuit-breaker, approval, and blocked conditions.

Do not display the contract as a substitute for execution. Make it visible only when useful for user steering, or persist it when durable state is warranted.

Use a rolling milestone plan, not a speculative exhaustive DAG. Plan the near term precisely and later work at lower resolution; re-plan when evidence changes the path. Use a formal dependency graph only when real parallel dependencies make it useful. Apply a short pre-mortem only to high-risk legs, identifying likely failure signals and concrete mitigations.

## Externalize durable state

For work expected to cross a context refresh, multiple goal continuations, or a handoff—and when local writes are in scope—prefer the project's existing planning convention. Otherwise create a task-scoped directory such as `.codex/long-horizon/<goal-slug>/` in the in-scope workspace. Read [the durable-state template](references/durable-state.md) before creating it.

Keep two concise sources of truth:

- `CONTRACT.md`: stable outcome, constraints, non-goals, definition of done, and approval boundaries. Amend it only when user direction or verified evidence changes the contract.
- `STATE.md`: current milestone, completed work with evidence, decisions, changed artifacts, validation results, retry counters, blockers, and exact next actions.

Rewrite `STATE.md` into a compact current snapshot after major milestones or before a continuation; do not append raw logs indefinitely. Preserve exact commands, file paths, IDs, errors, and citations only when they are needed to reproduce, verify, or resume. Re-read the contract and state after compaction or a fresh continuation before acting.

Do not introduce Redis, a database, XML-wrapped output, or another orchestrator merely to manage one Codex goal. Add infrastructure only when the requested system itself needs concurrent coordination, machine parsing, or durable cross-process state.

## Execute milestone loops

For each milestone:

1. Confirm its acceptance criteria, dependencies, and risk triggers.
2. Inspect just enough context to choose the next action.
3. Implement the smallest coherent vertical slice.
4. Run the most relevant available checks and inspect their actual output.
5. Repair failures before building dependent work.
6. Perform a brief adversarial review against the contract, regression risk, and evidence.
7. Update durable state, then continue without waiting for routine approval.

Use targeted validation during development and broader integration or end-to-end validation at appropriate boundaries. “The command ran,” “the code compiles,” and visual plausibility are not proof unless they are the stated acceptance bar. If a check cannot run, record why and use the strongest available substitute.

Use separate workers or reviewers only when the harness permits them and the work divides into genuinely independent streams with clear ownership and merge criteria. Keep a single accountable owner for the end-to-end result. Do not add agents merely to appear thorough.

## Configure guardrails and explicit stop points

Derive concrete stop checks from the task before starting risky work. These defaults always apply:

- **Transient tool failure:** allow at most three total occurrences of the same failure signature. Retry only after collecting new evidence or changing a relevant parameter.
- **Repair failure:** allow at most three materially distinct hypotheses for the same validation failure. Repeating the same edit or command with cosmetic variation is not a new attempt.
- **No-progress breaker:** trip when three consecutive execution cycles produce neither a validated delta nor new evidence that changes the diagnosis.
- **Scope breaker:** re-plan before continuing when the required work materially exceeds the contract, invalidates a core architecture assumption, or would consume an explicit budget unexpectedly.
- **Safety breaker:** stop before destructive, external, costly, security-sensitive, privacy-sensitive, or irreversible action that lacks clear authority.
- **Completion stop:** stop when every required deliverable and acceptance criterion has evidence. Do not continue optional polishing, refactoring, or feature expansion after done.

When a breaker trips, stop repeating the affected action. Preserve the last known-good state and record the failure signature, evidence, attempts, and remaining hypotheses. Try one safe alternative path only if it is materially different and remains within scope. If the failure is on the critical path and no safe alternative remains, halt the run with an exact unblock requirement; do not claim partial work is complete. Obey any stricter Goal-mode rule for when the goal may formally be marked blocked.

Never ping a webhook, message a person, purchase resources, change production, or perform another external mutation unless the user authorized that action. A terminal request such as “keep going” authorizes persistence, not expanded permissions.

## Counter GPT-5.6 SOL failure modes

- Keep the contract lean. State each invariant once; remove motivational prose, duplicated rules, and examples that do not change decisions.
- Specify the outcome, evidence, autonomy, and stopping bar; leave ordinary path selection to the model.
- Do not request hidden chain-of-thought, “extensive reflection,” or `<thought>` output. Use concise decisions, evidence, and state updates.
- Do not over-compress the final result: preserve required evidence, caveats, decisions, and next actions.
- Do not mistake persistence for endless exploration. Retry budgets and completion criteria outrank generic instructions to keep going.
- Do not let stale plans or prior reasoning override new test results, user steering, or repository evidence.
- Do not ask repeatedly for approval. Ask only at the actual boundary that requires it.
- Do not mark work complete because a plausible implementation exists; require the defined evidence.

## Finish or hand off

Mark the goal complete only after reconciling every acceptance criterion with evidence and checking for unresolved critical regressions. Report the delivered outcome, meaningful validation, material assumptions or caveats, and any intentionally deferred non-goal.

If stopped, report the last known-good checkpoint, the exact blocker, attempts already made, preserved artifacts, and the smallest user or external action that would unblock progress. Leave the durable state sufficient for another continuation to resume without reconstructing history.
