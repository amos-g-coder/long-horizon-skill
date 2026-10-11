# Durable state template

Use this only when a task is likely to survive multiple context cycles or handoffs and local state-file writes are authorized. Adapt it to an existing project convention rather than creating duplicate planning systems.

## `CONTRACT.md`

```markdown
# Execution contract: <goal>

## Outcome
<One concrete end state.>

## Deliverables
- [ ] <Artifact or observable change>

## Definition of done
- [ ] <Acceptance criterion> — Evidence: <test, inspection, source, or artifact>

## Scope
Included: <boundaries>
Non-goals: <explicit exclusions>
Preserve: <behavior or data that must not regress>

## Constraints and authority
- <Technical, safety, privacy, cost, compatibility, or deadline constraint>
- Allowed without approval: <safe in-scope actions>
- Approval required: <external, destructive, costly, or scope-expanding actions>

## Assumptions
- <Assumption> — Basis: <evidence/convention> — Validation: <check>

## Stop policy
- Completion: <evidence required before completion>
- Retry breaker: <failure signature and attempt limit>
- Hard stops: <authority, safety, contradiction, or critical-path conditions>
```

## `STATE.md`

```markdown
# Current state

Updated: <timestamp or continuation identifier>
Status: <active | awaiting approval | stopped | complete>
Current milestone: <name and intended outcome>

## Completed with evidence
- <Result> — <command/result, artifact, source, or inspection>

## Current facts and decisions
- <Decision> — Why: <short rationale> — Revisit if: <trigger>

## Changed artifacts
- `<path or ID>` — <purpose/status>

## Validation
- PASS: `<command/check>` — <result>
- FAIL: `<command/check>` — <failure signature>
- NOT RUN: `<check>` — <reason and substitute>

## Retry and breaker state
- Failure signature: <stable concise identifier>
- Attempts: <count>/<limit>
- Distinct hypotheses tried: <list>
- Breaker status: <closed | open>

## Blockers and risks
- <Blocker/risk> — Signal: <evidence> — Unblock/mitigation: <exact action>

## Next actions
1. <Smallest executable next step>
2. <Following dependency-aware step>
```

## State hygiene

- Treat `CONTRACT.md` as stable and `STATE.md` as replaceable working memory.
- Update state after a validated milestone, a material decision, a breaker, or before yielding across a continuation.
- Keep facts and evidence, not a transcript. Replace obsolete state rather than accumulating history.
- Preserve a decision only while its rationale and revisit trigger remain relevant.
- Link to large logs or artifacts instead of copying them into state.
- On resume, read the contract and current state, verify the workspace still matches the snapshot, then continue from the first incomplete acceptance criterion.
