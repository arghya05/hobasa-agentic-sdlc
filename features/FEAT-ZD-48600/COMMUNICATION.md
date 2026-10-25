# Communication for FEAT-ZD-48600

**FEAT-ZD-48600** — Zendesk ticket ZD-48600 (sample, synthetic) (Customer Feedback)

AP managers want to see which overdue invoices belong to vendors that usually pay late, so they can chase them first. (1) Data engineering, ap_pipeline: the vendor feed gains an optional paid_date column (ISO date, empty when unpaid); an invalid paid_date rejects the row with reason 'paid_date'; add delays_by_vendor(records) returning {vendor: [delay_days, ...]} for paid records with a paid_date, where delay_days = (paid_date - due_date) in days, in feed order. (2) AI / data science, ap_forecast: add vendor_risk(history) returning 'high' when predict_delay_days(history) > 30, 'medium' when it is > 10, otherwise 'low'; build_explanation_request gains an optional risk argument and, when given, the prompt ends with ' Risk level: <risk>.'. (3) Backend, ap_aging: add overdue_with_risk(invoices, as_of, risk_by_vendor) returning, for unpaid invoices more than 30 days past due, a list of {'id', 'vendor', 'days', 'amount', 'risk'} sorted by days descending then id, with risk 'unknown' for vendors not in risk_by_vendor. (4) Frontend, ap_portal: add renderOverdueRisk(rows) rendering '<table class="overdue-risk">' with one '<tr class="risk-RISK">' per row showing id, vendor, days and amount to two decimals, and an empty string when there are no rows. The whole flow must be proven end to end: feed -> delays -> risk -> overdue list -> portal table.

Gates: SIMULATED (automated test). Journey board: https://github.com/arghya05/hobasa-agentic-sdlc/blob/main/features/FEAT-ZD-48600/JOURNEY.md

Decide in this issue: `/approve <STEP> <role> scores=c,c,g,u <comment>`, `/reject <STEP> <role>: <reason>`, `/answer <STEP>: <text>` (scores: correct, complete, grounded, useful, 1-5).

---
**2026-10-25 12:56:06**

⏸ **Gate REQ-07 Technical Requirement Document** needs **Architect**. Review [feat.trd](https://github.com/arghya05/hobasa-requirement-agent/blob/main/outputs/FEAT-ZD-48600/feat.trd.md) and the [step record](https://github.com/arghya05/hobasa-requirement-agent/blob/main/steps/FEAT-ZD-48600/REQ-07/README.md) (checks and independent judge passed). Reply `/approve REQ-07 Architect scores=c,c,g,u <comment>` or `/reject REQ-07 Architect: <reason>`. *(SIMULATED gate: an automated approver decides on measurable criteria.)*

---
**2026-10-25 12:56:08**

✅ **REQ-07 Technical Requirement Document** (Requirement agent): done. Outputs: [feat.trd](https://github.com/arghya05/hobasa-requirement-agent/blob/main/outputs/FEAT-ZD-48600/feat.trd.md). [Inputs, attempts, checks and judge](https://github.com/arghya05/hobasa-requirement-agent/blob/main/steps/FEAT-ZD-48600/REQ-07/README.md). Decisions: Architect: approve by sim.architect.

---
**2026-10-25 13:08:24**

⏸ **Gate REQ-08 User Story Preparation** needs **PM**. Review [feat.stories](https://github.com/arghya05/hobasa-requirement-agent/blob/main/outputs/FEAT-ZD-48600/feat.stories.md) and the [step record](https://github.com/arghya05/hobasa-requirement-agent/blob/main/steps/FEAT-ZD-48600/REQ-08/README.md) (checks and independent judge passed). Reply `/approve REQ-08 PM scores=c,c,g,u <comment>` or `/reject REQ-08 PM: <reason>`. *(SIMULATED gate: an automated approver decides on measurable criteria.)*

---
**2026-10-25 13:08:25**

✅ **REQ-08 User Story Preparation** (Requirement agent): done. Outputs: [feat.stories](https://github.com/arghya05/hobasa-requirement-agent/blob/main/outputs/FEAT-ZD-48600/feat.stories.md). [Inputs, attempts, checks and judge](https://github.com/arghya05/hobasa-requirement-agent/blob/main/steps/FEAT-ZD-48600/REQ-08/README.md). Decisions: PM: approve by sim.pm.

---
**2026-10-25 13:10:43**

🔎 **DES-01 Platform Architecture Update ¹** (Design agent): checked. Outputs: [feat.platform_update](https://github.com/arghya05/hobasa-design-agent/blob/main/outputs/FEAT-ZD-48600/checks/DES-01_feat.platform_update.md). [Inputs, attempts, checks and judge](https://github.com/arghya05/hobasa-design-agent/blob/main/steps/FEAT-ZD-48600/DES-01/README.md).

---
**2026-10-25 13:20:51**

⏸ **Gate DES-02 Design Document** needs **Architect**. Review [feat.design](https://github.com/arghya05/hobasa-design-agent/blob/main/outputs/FEAT-ZD-48600/feat.design.md), [feat.screens](https://github.com/arghya05/hobasa-design-agent/blob/main/outputs/FEAT-ZD-48600/feat.screens.md) and the [step record](https://github.com/arghya05/hobasa-design-agent/blob/main/steps/FEAT-ZD-48600/DES-02/README.md) (checks and independent judge passed). Reply `/approve DES-02 Architect scores=c,c,g,u <comment>` or `/reject DES-02 Architect: <reason>`. *(SIMULATED gate: an automated approver decides on measurable criteria.)*

---
**2026-10-25 13:20:53**

⏸ **Gate DES-02 Design Document** needs **UX lead**. Review [feat.design](https://github.com/arghya05/hobasa-design-agent/blob/main/outputs/FEAT-ZD-48600/feat.design.md), [feat.screens](https://github.com/arghya05/hobasa-design-agent/blob/main/outputs/FEAT-ZD-48600/feat.screens.md) and the [step record](https://github.com/arghya05/hobasa-design-agent/blob/main/steps/FEAT-ZD-48600/DES-02/README.md) (checks and independent judge passed). Reply `/approve DES-02 UX lead scores=c,c,g,u <comment>` or `/reject DES-02 UX lead: <reason>`. *(SIMULATED gate: an automated approver decides on measurable criteria.)*

---
**2026-10-25 13:20:54**

✅ **DES-02 Design Document** (Design agent): done. Outputs: [feat.design](https://github.com/arghya05/hobasa-design-agent/blob/main/outputs/FEAT-ZD-48600/feat.design.md), [feat.screens](https://github.com/arghya05/hobasa-design-agent/blob/main/outputs/FEAT-ZD-48600/feat.screens.md). [Inputs, attempts, checks and judge](https://github.com/arghya05/hobasa-design-agent/blob/main/steps/FEAT-ZD-48600/DES-02/README.md). Decisions: Architect: approve by sim.architect; UX lead: approve by sim.ux_lead.

---
**2026-10-25 13:29:35**

⏸ **Gate DES-03 Understand HLD or LLD+ Doubts Clarifications** needs **Architect**. Review [feat.clarifications](https://github.com/arghya05/hobasa-design-agent/blob/main/outputs/FEAT-ZD-48600/feat.clarifications.md) and the [step record](https://github.com/arghya05/hobasa-design-agent/blob/main/steps/FEAT-ZD-48600/DES-03/README.md) (checks and independent judge passed). Reply `/approve DES-03 Architect scores=c,c,g,u <comment>` or `/reject DES-03 Architect: <reason>`. *(SIMULATED gate: an automated approver decides on measurable criteria.)*

---
**2026-10-25 13:29:37**

✅ **DES-03 Understand HLD or LLD+ Doubts Clarifications** (Design agent): done. Outputs: [feat.clarifications](https://github.com/arghya05/hobasa-design-agent/blob/main/outputs/FEAT-ZD-48600/feat.clarifications.md). [Inputs, attempts, checks and judge](https://github.com/arghya05/hobasa-design-agent/blob/main/steps/FEAT-ZD-48600/DES-03/README.md). Decisions: Architect: approve by sim.architect.

---
**2026-10-25 13:35:29**

⏸ **Gate DES-04 Task Creation** needs **Developer**. Review [feat.tasks](https://github.com/arghya05/hobasa-design-agent/blob/main/outputs/FEAT-ZD-48600/feat.tasks.md), [feat.tier](https://github.com/arghya05/hobasa-design-agent/blob/main/outputs/FEAT-ZD-48600/feat.tier.md) and the [step record](https://github.com/arghya05/hobasa-design-agent/blob/main/steps/FEAT-ZD-48600/DES-04/README.md) (checks and independent judge passed). Reply `/approve DES-04 Developer scores=c,c,g,u <comment>` or `/reject DES-04 Developer: <reason>`. *(SIMULATED gate: an automated approver decides on measurable criteria.)*

---
**2026-10-25 13:35:30**

✅ **DES-04 Task Creation** (Design agent): done. Outputs: [feat.tasks](https://github.com/arghya05/hobasa-design-agent/blob/main/outputs/FEAT-ZD-48600/feat.tasks.md), [feat.tier](https://github.com/arghya05/hobasa-design-agent/blob/main/outputs/FEAT-ZD-48600/feat.tier.md). [Inputs, attempts, checks and judge](https://github.com/arghya05/hobasa-design-agent/blob/main/steps/FEAT-ZD-48600/DES-04/README.md). Decisions: Developer: approve by sim.developer.

---
**2026-10-25 13:38:27**

✅ **BE-01 Checking the coding prerequisites ⁶** (Backend agent): done. Outputs: [task.repo_access](https://github.com/arghya05/hobasa-backend-agent/blob/main/outputs/FEAT-ZD-48600/task.repo_access.md). [Inputs, attempts, checks and judge](https://github.com/arghya05/hobasa-backend-agent/blob/main/steps/FEAT-ZD-48600/BE-01/README.md).
