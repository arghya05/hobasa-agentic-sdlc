# Evaluation across the journey: FEAT-ZD-48600

**Gates:** SIMULATED (automated test) · **mode:** agentic (Claude Code sessions on your login) · **outcome:** REQ-04 ended blocked

## Zero hallucination

- Agent attempts: 10; problems caught by the guardrails and the independent judge before any person saw them: **13** (G1 judge: 9, G2: 4, G3: 0, G5: 0, G9: 0)
- Unsupported statements that reached a person: **0** (a gate opens only when every claim is backed by a read receipt, every number appears in its source, every output exists and the judge found nothing unsupported)
- Hook denials (writes outside the step, secrets, shell outside the allowlist, open web): 5
- Connector calls (logged and citable): 0; connector requests to approve: 0

## Evaluations

- Independent judge runs: 8; average scores {'correct': 4.88, 'complete': 4.25, 'grounded': 4.5, 'useful': 4.5}
- Human gate decisions: 0 (0 rejections); average human scores None
- Simulated decisions (automated test only): 4
- Sampled human evaluations: 0 done, 0 open

## Per step

| Step | Agent | Attempt | Approach | Tools used | Checks failed | Judge unsupported | Judge scores |
|---|---|---|---|---|---|---|---|
| REQ-01 | Requirement | 1 | I loaded the requirement-steps procedure for REQ-01, then read the five contracted inputs (roadmap, regulatory sources, connector inventory, model dependency ma | Skill:requirement-steps, Read, Glob, Grep, Write | 3 | — | — |
| REQ-01 | Requirement | 2 (resumed) | Attempt 2 fixes all three G2 refusals. In attempt 1 I had only seen requirements/ZD-48211.md, ZD-48501.md and ZD-48455.md as Grep matches and never read them. T | Skill:requirement-steps, Read, Glob, Grep, Write | 1 | 1 | {'correct': 5, 'complete': 4, 'grounded': 4, 'useful': 5} |
| REQ-01 | Requirement | 3 (resumed) | Attempt 3 fixes the G1 refusal on the connector check. I removed the blanket sentence "No source-system connector is affected". The connector row in feat.prebac | Skill:requirement-steps, Read, Glob, Grep, Write | 0 | 0 | {'correct': 5, 'complete': 4, 'grounded': 5, 'useful': 5} |
| REQ-02 | Requirement | 1 | I loaded the requirement-steps procedure for REQ-02, then read the four contracted inputs: feat.prebacklog, feat.intake, org.routing_map and org.architecture. I | Skill:requirement-steps, Read, Glob, Grep, Write, Edit | 2 | 2 | {'correct': 5, 'complete': 5, 'grounded': 4, 'useful': 5} |
| REQ-02 | Requirement | 2 (resumed) | Attempt 2 fixes both G1 refusals, and I rewrote feat.classification in full. (1) In the ZD-48470 overlap row I removed the inferred claim that both changes use  | Skill:requirement-steps, Read, Glob, Grep, Write, Edit | 0 | 0 | {'correct': 5, 'complete': 4, 'grounded': 5, 'useful': 4} |
| REQ-03 | Requirement | 1 | I followed the REQ-03 procedure in the requirement-steps skill and checked the entry against the roadmap, the capability and the strategy. I read the three cont | Skill:requirement-steps, Read, Glob, mcp__hobasa-context__context_list, mcp__hobasa-context__context_get, mcp__hobasa-co | 2 | 2 | {'correct': 5, 'complete': 4, 'grounded': 5, 'useful': 4} |
| REQ-03 | Requirement | 2 (resumed) | Attempt 2 fixes both G1 refusals, and I rewrote feat.fitment in full.

(1) I removed the claim that the entry supports 'help finance teams pay on time and avoid | Skill:requirement-steps, Read, mcp__hobasa-context__context_list, mcp__hobasa-context__context_get, mcp__hobasa-context_ | 0 | 0 | {'correct': 5, 'complete': 4, 'grounded': 5, 'useful': 4} |
| REQ-04 | Requirement | 1 | I read the five contracted inputs: feat.fitment, feat.intake, org.templates, org.strategy_capability and org.decision_log. I also read two approved background o | Skill:requirement-steps, Read, Glob, mcp__hobasa-context__context_list, mcp__hobasa-context__context_get, mcp__hobasa-co | 1 | — | — |
| REQ-04 | Requirement | 2 (resumed) | Attempt 2 fixes the G2 refusal. Attempt 1 cited mcp:hobasa-context in three places: the section 9 intro, B-A4 and OQ-B7. I replaced all three with record:brief. | Skill:requirement-steps, Read, Glob, Grep, mcp__hobasa-context__context_list, mcp__hobasa-context__context_get, mcp__hob | 3 | 3 | {'correct': 4, 'complete': 4, 'grounded': 4, 'useful': 4} |
| REQ-04 | Requirement | 3 (resumed) | Attempt 3 fixes the three G1 refusals, and I rewrote feat.brd in full. (1) Header: I removed the uncited sentence "Leadership approves; the PM owns the item". T | Skill:requirement-steps, Read, Glob, Grep, mcp__hobasa-context__context_list, mcp__hobasa-context__context_get, mcp__hob | 1 | 1 | {'correct': 5, 'complete': 5, 'grounded': 4, 'useful': 5} |
