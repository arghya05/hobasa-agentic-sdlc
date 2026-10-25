# Evaluation across the journey: FEAT-ZD-48600

**Gates:** SIMULATED (automated test) · **mode:** agentic (Claude Code sessions on your login) · **outcome:** REQ-07 ended blocked

## Zero hallucination

- Agent attempts: 28; problems caught by the guardrails and the independent judge before any person saw them: **77** (G1 judge: 37, G2: 39, G3: 1, G5: 0, G9: 0)
- Unsupported statements that reached a person: **0** (a gate opens only when every claim is backed by a read receipt, every number appears in its source, every output exists and the judge found nothing unsupported)
- Hook denials (writes outside the step, secrets, shell outside the allowlist, open web): 24
- Connector calls (logged and citable): 0; connector requests to approve: 0

## Evaluations

- Independent judge runs: 21; average scores {'correct': 4.71, 'complete': 4.48, 'grounded': 4.33, 'useful': 4.62}
- Human gate decisions: 0 (0 rejections); average human scores None
- Simulated decisions (automated test only): 7
- Sampled human evaluations: 0 done, 0 open

## Per step

| Step | Agent | Attempt | Approach | Tools used | Checks failed | Judge unsupported | Judge scores |
|---|---|---|---|---|---|---|---|
| REQ-01 | Requirement | 1 | I loaded the requirement-steps procedure for REQ-01. I read the five contracted inputs (roadmap, regulatory sources, connector inventory, model dependency map,  | Skill:requirement-steps, Read, Glob, Grep, Write | 5 | 5 | {'correct': 4, 'complete': 3, 'grounded': 4, 'useful': 4} |
| REQ-01 | Requirement | 2 (resumed) | Attempt 2 fixes all five refusal reasons:
1. Title: replaced with a near-quote of the ticket ("Show which overdue invoices belong to vendors that usually pay la | Skill:requirement-steps, Read, Glob, Grep, Write, ToolSearch, mcp__hobasa-context__capabilities_list, mcp__hobasa-contex | 1 | 1 | {'correct': 4, 'complete': 4, 'grounded': 4, 'useful': 4} |
| REQ-01 | Requirement | 3 (resumed) | Attempt 3 fixes the one refusal reason. A-2 said amounts were formatted to two decimals "only when rendered". That contradicted the architecture override in req | Skill:requirement-steps, Read, Glob, Grep, Write, ToolSearch, mcp__hobasa-context__capabilities_list, mcp__hobasa-contex | 0 | 0 | {'correct': 5, 'complete': 4, 'grounded': 5, 'useful': 5} |
| REQ-02 | Requirement | 1 | Ran the requirement-steps skill for REQ-02. Read the four contracted inputs: feat.prebacklog, feat.intake, the feature routing map and the feature architecture. | Skill:requirement-steps, Read, Glob, Grep, Write, Edit, Agent:verifier | 4 | — | — |
| REQ-02 | Requirement | 2 (resumed) | Attempt 2 fixes the G2 refusals. In attempt 1 the other requirement files were scanned with Grep only, so the check found no Read receipt for them. This time I  | Skill:requirement-steps, Read, Glob, Grep, Write, Edit, Agent:verifier | 1 | 1 | {'correct': 5, 'complete': 5, 'grounded': 5, 'useful': 5} |
| REQ-02 | Requirement | 3 (resumed) | Attempt 3 fixes the G1 refusal. The CR-4 row said without qualification that provider acme-llm and model acme-text-2 do not change. That overstated feat.preback | Skill:requirement-steps, Read, Glob, Grep, Write, Edit, Agent:verifier | 2 | 2 | {'correct': 5, 'complete': 5, 'grounded': 4, 'useful': 5} |
| REQ-02 | Requirement | 1 (resumed) | This attempt fixes the two G1 refusals. First, I removed the sentence saying the pre-backlog status "stays Draft entry for review". REQ-01 was approved at the P | Skill:requirement-steps, Read, Glob, Grep, Write, Edit, Agent:verifier | 1 | 1 | {'correct': 5, 'complete': 5, 'grounded': 4, 'useful': 5} |
| REQ-02 | Requirement | 2 (resumed) | This attempt fixes the G1 refusal. FIN-OPS-2026-07 had been listed among the related items said to share a rule or code with ZD-48600. It is a configuration-onl | Skill:requirement-steps, Read, Glob, Grep, Write, Edit, Agent:verifier | 0 | 0 | {'correct': 5, 'complete': 5, 'grounded': 5, 'useful': 5} |
| REQ-03 | Requirement | 1 | I read the three contracted inputs: feat.classification, org.strategy_capability and org.roadmap. I also read the source ticket file:hobasa-agentic-sdlc/require | Skill:requirement-steps, Read, Glob, Write | 3 | 3 | {'correct': 5, 'complete': 5, 'grounded': 4, 'useful': 5} |
| REQ-03 | Requirement | 2 (resumed) | Attempt 2 fixes the three G1 refusals and rewrites feat.fitment in full. (1) I removed "Nothing is inferred silently". The output now states only the sourced fa | Read, Write | 2 | 2 | {'correct': 4, 'complete': 5, 'grounded': 4, 'useful': 5} |
| REQ-03 | Requirement | 3 (resumed) | Attempt 3 fixes the two G1 refusals in feat.fitment; the rest of the file stays as approved in attempt 2. (1) I removed the claim that ap_pipeline, ap_forecast  | Read, Write, Edit | 1 | 1 | {'correct': 5, 'complete': 5, 'grounded': 4, 'useful': 5} |
| REQ-03 | Requirement | 1 (resumed) | This attempt fixes the single G1 refusal in feat.fitment. The sentence 'REQ-02 linked the entry to R-AP-12' wrongly said REQ-02 made the link. It now reads: 'fe | Read, Write, Edit, Grep | 0 | 0 | {'correct': 5, 'complete': 5, 'grounded': 5, 'useful': 4} |
| REQ-04 | Requirement | 1 | I read the five contracted inputs, the requirement-steps skill, and the approved background outputs (journey:feat.prebacklog and journey:feat.classification, bo | Skill:requirement-steps, Read, Glob, mcp__hobasa-context__context_list, mcp__hobasa-context__context_get, mcp__hobasa-co | 2 | 2 | {'correct': 5, 'complete': 4, 'grounded': 4, 'useful': 5} |
| REQ-04 | Requirement | 2 (resumed) | Attempt 2 fixes both refusal reasons, and feat.brd is rewritten in full. (1) Every citation that used the journey: prefix now uses the allowed file:<repository> | Skill:requirement-steps, Read, Glob, Grep, mcp__hobasa-context__context_list, mcp__hobasa-context__context_get, mcp__hob | 1 | 1 | {'correct': 5, 'complete': 5, 'grounded': 4, 'useful': 5} |
| REQ-04 | Requirement | 3 (resumed) | Attempt 3 fixes the single G1 refusal, and feat.brd is rewritten in full. SM-5 said "No existing function signature changes", which was stronger than the source | Skill:requirement-steps, Read, Glob, Grep, mcp__hobasa-context__context_list, mcp__hobasa-context__context_get, mcp__hob | 3 | 3 | {'correct': 4, 'complete': 5, 'grounded': 4, 'useful': 5} |
| REQ-04 | Requirement | 1 (resumed) | This attempt fixes all three G1 refusals and rewrites feat.brd in full.

1. SM-5 no longer says 'the only change to an existing function'. It now names both add | Skill:requirement-steps, Read, Glob, Grep, mcp__hobasa-context__context_list, mcp__hobasa-context__context_get, mcp__hob | 0 | 0 | {'correct': 5, 'complete': 4, 'grounded': 5, 'useful': 5} |
| REQ-05 | Requirement | 1 | I read the requirement-steps procedure for REQ-05 and the two contracted inputs, the approved feat.brd and org.templates. I also read the source ticket file to  | Skill (requirement-steps), Read, Write, Edit, Agent (verifier) | 1 | 1 | {'correct': 5, 'complete': 5, 'grounded': 5, 'useful': 5} |
| REQ-05 | Requirement | 2 (resumed) | Attempt 2 fixes the single G1 refusal. The old NFR-10, "Runtimes are unchanged: ... Python 3.9 ... Node.js 22 CommonJS", turned the runtime description in org.a | Skill (requirement-steps), Read, Write, Edit, Grep, Agent (verifier, attempt 1) | 0 | 0 | {'correct': 5, 'complete': 5, 'grounded': 5, 'useful': 5} |
| REQ-06 | Requirement | 1 | I loaded the requirement-steps skill for REQ-06. It reads feat.prd and org.design_library, writes feat.prototype, and the UX lead approves.

I read both inputs. | Skill (requirement-steps), Read, Grep, Glob, mcp__hobasa-context__capabilities_list, mcp__hobasa-context__memory_search, | 1 | — | — |
| REQ-06 | Requirement | 2 (resumed) | Attempt 2 fixes both G2 refusals and rewrites feat.prototype in full.

(1) file:ap_portal/src/ap_portal/index.js: I read the file again in this session, so the  | Read, Grep, Write | 1 | — | — |
| REQ-06 | Requirement | 3 (resumed) | Attempt 3 fixes the remaining G2 refusal. The citation file:ap_portal/src/ap_portal/index.js was not recognised as read in this step's context. So I removed it  | Read, Write, Grep | 2 | 2 | {'correct': 5, 'complete': 4, 'grounded': 4, 'useful': 4} |
| REQ-06 | Requirement | 1 (resumed) | Attempt 4 fixes both G1 refusals in feat.prototype. I re-read both contracted inputs and the current output first. The complete feat.prototype file is on disk;  | Read, Edit, Grep | 0 | 0 | {'correct': 5, 'complete': 4, 'grounded': 5, 'useful': 4} |
| REQ-07 | Requirement | 1 | I followed the requirement-steps procedure for REQ-07: draft the TRD from the PRD, the prototype and the current architecture, using the TRD template (component | Skill:requirement-steps, Read, Glob, mcp:hobasa-context memory_search, mcp:hobasa-context context_list, Write, Edit, Age | 13 | — | — |
| REQ-07 | Requirement | 2 (resumed) | Attempt 2 fixes all 13 G2 refusals. Each refusal cited a code file I had read in an earlier session, but not in the session that was checked.

1. In this sessio | Read, Write, Skill:requirement-steps (attempt 1), mcp:hobasa-context memory_search (attempt 1), mcp:hobasa-context conte | 19 | — | — |
| REQ-07 | Requirement | 3 (resumed) | Attempt 3 fixes all 19 G2 refusals. Every refused citation was to a file in one of the four app repositories (ap_pipeline, ap_forecast, ap_aging, ap_portal). In | mcp:hobasa-context context_get (feat.prd, feat.prototype, org.architecture), mcp:hobasa-context capabilities_list, api:g | 1 | — | — |
| REQ-07 | Requirement | 1 (resumed) | This attempt fixes the one refusal: a claim cited api:github, and no successful call to that API counted in the checked session.

I called the GitHub connector  | mcp:hobasa-context context_get (org.architecture), mcp:hobasa-context api_call (GitHub connector; credentials error, not | 6 | 6 | {'correct': 4, 'complete': 3, 'grounded': 3, 'useful': 4} |
| REQ-07 | Requirement | 2 (resumed) | This attempt fixes all six G1 points the judge raised.

1. TQ-12 said what a GitHub connector call returned, and there is no saved response for that. TQ-12 is r | Read, Glob, Write, Grep | 1 | — | — |
| REQ-07 | Requirement | 3 (resumed) | This attempt fixes the one G3 refusal. The claim that cited org.templates included the section numbers "2" and "7" ("sections 2 to 7"), and those numbers do not | Read, Write | 6 | 6 | {'correct': 4, 'complete': 4, 'grounded': 4, 'useful': 3} |
