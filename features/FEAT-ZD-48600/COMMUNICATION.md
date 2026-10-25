# Communication for FEAT-ZD-48600

**FEAT-ZD-48600** — Zendesk ticket ZD-48600 (sample, synthetic) (Customer Feedback)

AP managers want to see which overdue invoices belong to vendors that usually pay late, so they can chase them first. (1) Data engineering, ap_pipeline: the vendor feed gains an optional paid_date column (ISO date, empty when unpaid); an invalid paid_date rejects the row with reason 'paid_date'; add delays_by_vendor(records) returning {vendor: [delay_days, ...]} for paid records with a paid_date, where delay_days = (paid_date - due_date) in days, in feed order. (2) AI / data science, ap_forecast: add vendor_risk(history) returning 'high' when predict_delay_days(history) > 30, 'medium' when it is > 10, otherwise 'low'; build_explanation_request gains an optional risk argument and, when given, the prompt ends with ' Risk level: <risk>.'. (3) Backend, ap_aging: add overdue_with_risk(invoices, as_of, risk_by_vendor) returning, for unpaid invoices more than 30 days past due, a list of {'id', 'vendor', 'days', 'amount', 'risk'} sorted by days descending then id, with risk 'unknown' for vendors not in risk_by_vendor. (4) Frontend, ap_portal: add renderOverdueRisk(rows) rendering '<table class="overdue-risk">' with one '<tr class="risk-RISK">' per row showing id, vendor, days and amount to two decimals, and an empty string when there are no rows. The whole flow must be proven end to end: feed -> delays -> risk -> overdue list -> portal table.

Gates: SIMULATED (automated test). Journey board: https://github.com/arghya05/hobasa-agentic-sdlc/blob/main/features/FEAT-ZD-48600/JOURNEY.md

Decide in this issue: `/approve <STEP> <role> scores=c,c,g,u <comment>`, `/reject <STEP> <role>: <reason>`, `/answer <STEP>: <text>` (scores: correct, complete, grounded, useful, 1-5).

---
**2026-10-25 11:19:13**

⏸ **Gate REQ-01 Requirement Intake** needs **PM**. Review [feat.intake](https://github.com/arghya05/hobasa-requirement-agent/blob/main/outputs/FEAT-ZD-48600/feat.intake.md), [feat.prebacklog](https://github.com/arghya05/hobasa-requirement-agent/blob/main/outputs/FEAT-ZD-48600/feat.prebacklog.md) and the [step record](https://github.com/arghya05/hobasa-requirement-agent/blob/main/steps/FEAT-ZD-48600/REQ-01/README.md) (checks and independent judge passed). Reply `/approve REQ-01 PM scores=c,c,g,u <comment>` or `/reject REQ-01 PM: <reason>`. *(SIMULATED gate: an automated approver decides on measurable criteria.)*

---
**2026-10-25 11:19:15**

✅ **REQ-01 Requirement Intake** (Requirement agent): done. Outputs: [feat.intake](https://github.com/arghya05/hobasa-requirement-agent/blob/main/outputs/FEAT-ZD-48600/feat.intake.md), [feat.prebacklog](https://github.com/arghya05/hobasa-requirement-agent/blob/main/outputs/FEAT-ZD-48600/feat.prebacklog.md). [Inputs, attempts, checks and judge](https://github.com/arghya05/hobasa-requirement-agent/blob/main/steps/FEAT-ZD-48600/REQ-01/README.md). Decisions: PM: approve by sim.pm.

---
**2026-10-25 11:26:08**

⚠️ **REQ-02 blocked** after its bounded attempts. *SIMULATED exception resolution by PM: one more bounded round in the same session with every refusal reason.*

- G1 judge found an unsupported statement: "The pre-backlog entry status stays "Draft entry for review"." (feat.prebacklog does record the status as "Draft entry for review; gate: PM". But the workspace history (commit 0648784 "FEAT-ZD-48600 REQ-01 Requirement Intake)
- G1 judge found an unsupported statement: "The source item's own type tag is `New Feature`, which matches this classification." (In requirements/ZD-48600.md the field is `expected_type: New Feature`, an expected or oracle value, not a type tag on the ticket. The value is correct, but the )

---
**2026-10-25 11:30:01**

⏸ **Gate REQ-02 Grouping** needs **PM**. Review [feat.classification](https://github.com/arghya05/hobasa-requirement-agent/blob/main/outputs/FEAT-ZD-48600/feat.classification.md) and the [step record](https://github.com/arghya05/hobasa-requirement-agent/blob/main/steps/FEAT-ZD-48600/REQ-02/README.md) (checks and independent judge passed). Reply `/approve REQ-02 PM scores=c,c,g,u <comment>` or `/reject REQ-02 PM: <reason>`. *(SIMULATED gate: an automated approver decides on measurable criteria.)*

---
**2026-10-25 11:30:03**

✅ **REQ-02 Grouping** (Requirement agent): done. Outputs: [feat.classification](https://github.com/arghya05/hobasa-requirement-agent/blob/main/outputs/FEAT-ZD-48600/feat.classification.md). [Inputs, attempts, checks and judge](https://github.com/arghya05/hobasa-requirement-agent/blob/main/steps/FEAT-ZD-48600/REQ-02/README.md). Decisions: PM: approve by sim.pm.

---
**2026-10-25 11:35:00**

⚠️ **REQ-03 blocked** after its bounded attempts. *SIMULATED exception resolution by PM: one more bounded round in the same session with every refusal reason.*

- G1 judge found an unsupported statement: "REQ-02 linked the entry to R-AP-12." (feat.classification (the REQ-02 output) cites feat.prebacklog as the source of the Linked roadmap item R-AP-12 (lines 16 and 70). The link was made earlier, in )

---
**2026-10-25 11:36:14**

⏸ **Gate REQ-03 Product Fitment Validation** needs **PM**. Review [feat.fitment](https://github.com/arghya05/hobasa-requirement-agent/blob/main/outputs/FEAT-ZD-48600/feat.fitment.md) and the [step record](https://github.com/arghya05/hobasa-requirement-agent/blob/main/steps/FEAT-ZD-48600/REQ-03/README.md) (checks and independent judge passed). Reply `/approve REQ-03 PM scores=c,c,g,u <comment>` or `/reject REQ-03 PM: <reason>`. *(SIMULATED gate: an automated approver decides on measurable criteria.)*

---
**2026-10-25 11:36:16**

⏸ **Gate REQ-03 Product Fitment Validation** needs **Leadership**. Review [feat.fitment](https://github.com/arghya05/hobasa-requirement-agent/blob/main/outputs/FEAT-ZD-48600/feat.fitment.md) and the [step record](https://github.com/arghya05/hobasa-requirement-agent/blob/main/steps/FEAT-ZD-48600/REQ-03/README.md) (checks and independent judge passed). Reply `/approve REQ-03 Leadership scores=c,c,g,u <comment>` or `/reject REQ-03 Leadership: <reason>`. *(SIMULATED gate: an automated approver decides on measurable criteria.)*

---
**2026-10-25 11:36:17**

✅ **REQ-03 Product Fitment Validation** (Requirement agent): done. Outputs: [feat.fitment](https://github.com/arghya05/hobasa-requirement-agent/blob/main/outputs/FEAT-ZD-48600/feat.fitment.md). [Inputs, attempts, checks and judge](https://github.com/arghya05/hobasa-requirement-agent/blob/main/steps/FEAT-ZD-48600/REQ-03/README.md). Decisions: PM: approve by sim.pm; Leadership: approve by sim.leadership.

---
**2026-10-25 11:45:45**

⚠️ **REQ-04 blocked** after its bounded attempts. *SIMULATED exception resolution by PM: one more bounded round in the same session with every refusal reason.*

- G1 judge found an unsupported statement: "SM-5 | ... The new behaviour comes from new functions (`delays_by_vendor`, `vendor_risk`, `overdue_with_risk`, `renderOverdueRisk`). The only change to an exist" (The cited source says otherwise. feat.classification (line 27) says "Two changes touch existing
- G1 judge found an unsupported statement: "The outcome delivers the roadmap item R-AP-12, "give AP managers earlier visibility of overdue payables" (Q4 2026 roadmap, AP module)." (feat.fitment only says, as agent judgement, that the entry "matches" R-AP-12 and "fits" it. Saying it "delivers" the road
- G1 judge found an unsupported statement: "Every rule in this BRD is explicit. The vendor risk rule "uses no LLM; it is a rule on the predicted delay". An invalid `paid_date` is rejected with a named rea" (The quoted facts are supported. The claim that these support the auditability promise is labell

---
**2026-10-25 11:50:06**

⏸ **Gate REQ-04 BRD Preparation** needs **Leadership**. Review [feat.brd](https://github.com/arghya05/hobasa-requirement-agent/blob/main/outputs/FEAT-ZD-48600/feat.brd.md) and the [step record](https://github.com/arghya05/hobasa-requirement-agent/blob/main/steps/FEAT-ZD-48600/REQ-04/README.md) (checks and independent judge passed). Reply `/approve REQ-04 Leadership scores=c,c,g,u <comment>` or `/reject REQ-04 Leadership: <reason>`. *(SIMULATED gate: an automated approver decides on measurable criteria.)*

---
**2026-10-25 11:50:08**

✅ **REQ-04 BRD Preparation** (Requirement agent): done. Outputs: [feat.brd](https://github.com/arghya05/hobasa-requirement-agent/blob/main/outputs/FEAT-ZD-48600/feat.brd.md). [Inputs, attempts, checks and judge](https://github.com/arghya05/hobasa-requirement-agent/blob/main/steps/FEAT-ZD-48600/REQ-04/README.md). Decisions: Leadership: approve by sim.leadership.

---
**2026-10-25 11:57:30**

⏸ **Gate REQ-05 Product Requirement Preparation** needs **PM**. Review [feat.prd](https://github.com/arghya05/hobasa-requirement-agent/blob/main/outputs/FEAT-ZD-48600/feat.prd.md) and the [step record](https://github.com/arghya05/hobasa-requirement-agent/blob/main/steps/FEAT-ZD-48600/REQ-05/README.md) (checks and independent judge passed). Reply `/approve REQ-05 PM scores=c,c,g,u <comment>` or `/reject REQ-05 PM: <reason>`. *(SIMULATED gate: an automated approver decides on measurable criteria.)*

---
**2026-10-25 11:57:31**

✅ **REQ-05 Product Requirement Preparation** (Requirement agent): done. Outputs: [feat.prd](https://github.com/arghya05/hobasa-requirement-agent/blob/main/outputs/FEAT-ZD-48600/feat.prd.md). [Inputs, attempts, checks and judge](https://github.com/arghya05/hobasa-requirement-agent/blob/main/steps/FEAT-ZD-48600/REQ-05/README.md). Decisions: PM: approve by sim.pm.

---
**2026-10-25 12:05:09**

⚠️ **REQ-06 blocked** after its bounded attempts. *SIMULATED exception resolution by PM: one more bounded round in the same session with every refusal reason.*

- G1 judge found an unsupported statement: "No secrets or personal data in outputs (G8) | record:brief" (Neither the step brief nor any input mentions a gate or rule called "G8", or a rule against secrets or personal data. The only gate ID in the brief is G2, in th)
- G1 judge found an unsupported statement: "| SD-1 | Synthetic data only: ids prefixed `SYN-INV-`, vendor names "Synthetic Vendor <letter>"; no real vendor, person, bank or contact data | ... | record:bri" (The brief names synthetic data rules in the workbook action, but it defines none. Section 6 and

---
**2026-10-25 12:06:33**

⏸ **Gate REQ-06 Prototype ⁷** needs **UX lead**. Review [feat.prototype](https://github.com/arghya05/hobasa-requirement-agent/blob/main/outputs/FEAT-ZD-48600/feat.prototype.md) and the [step record](https://github.com/arghya05/hobasa-requirement-agent/blob/main/steps/FEAT-ZD-48600/REQ-06/README.md) (checks and independent judge passed). Reply `/approve REQ-06 UX lead scores=c,c,g,u <comment>` or `/reject REQ-06 UX lead: <reason>`. *(SIMULATED gate: an automated approver decides on measurable criteria.)*

---
**2026-10-25 12:06:34**

✅ **REQ-06 Prototype ⁷** (Requirement agent): done. Outputs: [feat.prototype](https://github.com/arghya05/hobasa-requirement-agent/blob/main/outputs/FEAT-ZD-48600/feat.prototype.md). [Inputs, attempts, checks and judge](https://github.com/arghya05/hobasa-requirement-agent/blob/main/steps/FEAT-ZD-48600/REQ-06/README.md). Decisions: UX lead: approve by sim.ux_lead.
