# Evaluation across the journey: FEAT-ZD-48600

**Gates:** SIMULATED (automated test) · **mode:** agentic (Claude Code sessions on your login) · **outcome:** REQ-02 ended blocked

## Zero hallucination

- Agent attempts: 6; problems caught by the guardrails and the independent judge before any person saw them: **17** (G1 judge: 16, G2: 0, G3: 1, G5: 0, G9: 0)
- Unsupported statements that reached a person: **0** (a gate opens only when every claim is backed by a read receipt, every number appears in its source, every output exists and the judge found nothing unsupported)
- Hook denials (writes outside the step, secrets, shell outside the allowlist, open web): 3
- Connector calls (logged and citable): 0; connector requests to approve: 0

## Evaluations

- Independent judge runs: 5; average scores {'correct': 4.2, 'complete': 3.8, 'grounded': 4.0, 'useful': 4.2}
- Human gate decisions: 0 (0 rejections); average human scores None
- Simulated decisions (automated test only): 1
- Sampled human evaluations: 0 done, 0 open

## Per step

| Step | Agent | Attempt | Approach | Tools used | Checks failed | Judge unsupported | Judge scores |
|---|---|---|---|---|---|---|---|
| REQ-01 | Requirement | 1 | I followed the requirement-steps REQ-01 procedure for a ticket intake. I read the Zendesk ticket from the trigger record and the five contracted inputs (roadmap | Skill:requirement-steps, Read, Glob, mcp__hobasa-context__context_list, mcp__hobasa-context__memory_search, Write, Edit | 5 | 5 | {'correct': 4, 'complete': 4, 'grounded': 4, 'useful': 4} |
| REQ-01 | Requirement | 2 (resumed) | Attempt 2 rewrites both files in full to fix all five G1 refusals. I removed every statement the inputs and brief do not support: the names of later steps (REQ- | Skill:requirement-steps, Read, Glob, mcp__hobasa-context__context_list, mcp__hobasa-context__memory_search, Write, Edit | 1 | 1 | {'correct': 5, 'complete': 4, 'grounded': 5, 'useful': 5} |
| REQ-01 | Requirement | 3 (resumed) | Attempt 3 rewrites both files in full and fixes the one remaining G1 refusal. D-2026-031 is now applied only to overdue_with_risk in ap_aging, which is the agin | Skill:requirement-steps, Read, Glob, mcp__hobasa-context__context_list, mcp__hobasa-context__memory_search, Write, Edit | 0 | 0 | {'correct': 5, 'complete': 4, 'grounded': 5, 'useful': 5} |
| REQ-02 | Requirement | 1 | I followed the requirement-steps REQ-02 procedure. First I read the two contracted inputs (feat.prebacklog, feat.intake), the org routing map and the feature-le | Skill:requirement-steps, Read, Glob, Grep, mcp__hobasa-context__context_list, mcp__hobasa-context__memory_search, Write | 1 | — | — |
| REQ-02 | Requirement | 2 (resumed) | Attempt 2 fixes every refusal point and rewrites feat.classification.md in full. (1) G2: claims now cite only sources this step accepts, which are feat.intake,  | Skill:requirement-steps, Read, Grep, mcp__hobasa-context__context_list, mcp__hobasa-context__context_get, mcp__hobasa-co | 7 | 7 | {'correct': 4, 'complete': 4, 'grounded': 2, 'useful': 4} |
| REQ-02 | Requirement | 3 (resumed) | Attempt 3 rewrites feat.classification.md in full so that every statement rests only on feat.intake, feat.prebacklog, record:brief or record:memory. I removed a | Skill:requirement-steps, Read, mcp__hobasa-context__context_list, mcp__hobasa-context__context_get, mcp__hobasa-context_ | 3 | 3 | {'correct': 3, 'complete': 3, 'grounded': 4, 'useful': 3} |
