# Communication for FEAT-ZD-48600

**FEAT-ZD-48600** — Zendesk ticket ZD-48600 (sample, synthetic) (Customer Feedback)

AP managers want to see which overdue invoices belong to vendors that usually pay late, so they can chase them first. (1) Data engineering, ap_pipeline: the vendor feed gains an optional paid_date column (ISO date, empty when unpaid); an invalid paid_date rejects the row with reason 'paid_date'; add delays_by_vendor(records) returning {vendor: [delay_days, ...]} for paid records with a paid_date, where delay_days = (paid_date - due_date) in days, in feed order. (2) AI / data science, ap_forecast: add vendor_risk(history) returning 'high' when predict_delay_days(history) > 30, 'medium' when it is > 10, otherwise 'low'; build_explanation_request gains an optional risk argument and, when given, the prompt ends with ' Risk level: <risk>.'. (3) Backend, ap_aging: add overdue_with_risk(invoices, as_of, risk_by_vendor) returning, for unpaid invoices more than 30 days past due, a list of {'id', 'vendor', 'days', 'amount', 'risk'} sorted by days descending then id, with risk 'unknown' for vendors not in risk_by_vendor. (4) Frontend, ap_portal: add renderOverdueRisk(rows) rendering '<table class="overdue-risk">' with one '<tr class="risk-RISK">' per row showing id, vendor, days and amount to two decimals, and an empty string when there are no rows. The whole flow must be proven end to end: feed -> delays -> risk -> overdue list -> portal table.

Gates: SIMULATED (automated test). Journey board: https://github.com/arghya05/hobasa-agentic-sdlc/blob/main/features/FEAT-ZD-48600/JOURNEY.md

Decide in this issue: `/approve <STEP> <role> scores=c,c,g,u <comment>`, `/reject <STEP> <role>: <reason>`, `/answer <STEP>: <text>` (scores: correct, complete, grounded, useful, 1-5).

---
**2026-10-25 20:57:34**

🔎 **DES-01 Platform Architecture Update ¹** (Design agent): checked. Outputs: [feat.platform_update](https://github.com/arghya05/hobasa-design-agent/blob/main/outputs/FEAT-ZD-48600/checks/DES-01_feat.platform_update.md). [Inputs, attempts, checks and judge](https://github.com/arghya05/hobasa-design-agent/blob/main/steps/FEAT-ZD-48600/DES-01/README.md).

---
**2026-10-25 20:59:29**

✅ **BE-01 Checking the coding prerequisites ⁶** (Backend agent): done. Outputs: [task.repo_access](https://github.com/arghya05/hobasa-backend-agent/blob/main/outputs/FEAT-ZD-48600/task.repo_access.md). [Inputs, attempts, checks and judge](https://github.com/arghya05/hobasa-backend-agent/blob/main/steps/FEAT-ZD-48600/BE-01/README.md).

---
**2026-10-25 20:59:47**

✅ **FE-01 Checking the coding prerequisites ⁶** (Frontend agent): done. Outputs: [task.repo_access](https://github.com/arghya05/hobasa-frontend-agent/blob/main/outputs/FEAT-ZD-48600/task.repo_access.md). [Inputs, attempts, checks and judge](https://github.com/arghya05/hobasa-frontend-agent/blob/main/steps/FEAT-ZD-48600/FE-01/README.md).

---
**2026-10-25 21:00:37**

⏸ **Gate DE-01 Checking the coding prerequisites ⁹** needs **Data engineer**. Review [task.repo_access](https://github.com/arghya05/hobasa-data-engineering-agent/blob/main/outputs/FEAT-ZD-48600/task.repo_access.md) and the [step record](https://github.com/arghya05/hobasa-data-engineering-agent/blob/main/steps/FEAT-ZD-48600/DE-01/README.md) (checks and independent judge passed). Reply `/approve DE-01 Data engineer scores=c,c,g,u <comment>` or `/reject DE-01 Data engineer: <reason>`. *(SIMULATED gate: an automated approver decides on measurable criteria.)*

---
**2026-10-25 21:00:39**

✅ **DE-01 Checking the coding prerequisites ⁹** (Data Engineering agent): done. Outputs: [task.repo_access](https://github.com/arghya05/hobasa-data-engineering-agent/blob/main/outputs/FEAT-ZD-48600/task.repo_access.md). [Inputs, attempts, checks and judge](https://github.com/arghya05/hobasa-data-engineering-agent/blob/main/steps/FEAT-ZD-48600/DE-01/README.md). Decisions: Data engineer: approve by sim.data_engineer.

---
**2026-10-25 21:01:00**

✅ **DS-01 Checking the coding prerequisites ⁶** (Data Science agent): done. Outputs: [task.repo_access](https://github.com/arghya05/hobasa-data-science-agent/blob/main/outputs/FEAT-ZD-48600/task.repo_access.md). [Inputs, attempts, checks and judge](https://github.com/arghya05/hobasa-data-science-agent/blob/main/steps/FEAT-ZD-48600/DS-01/README.md).

---
**2026-10-25 21:02:03**

✅ **FE-02 Access to secrets** (Frontend agent): done. Outputs: [task.secrets_scope](https://github.com/arghya05/hobasa-frontend-agent/blob/main/outputs/FEAT-ZD-48600/task.secrets_scope.md). [Inputs, attempts, checks and judge](https://github.com/arghya05/hobasa-frontend-agent/blob/main/steps/FEAT-ZD-48600/FE-02/README.md).

---
**2026-10-25 21:02:23**

✅ **BE-02 Access to secrets** (Backend agent): done. Outputs: [task.secrets_scope](https://github.com/arghya05/hobasa-backend-agent/blob/main/outputs/FEAT-ZD-48600/task.secrets_scope.md). [Inputs, attempts, checks and judge](https://github.com/arghya05/hobasa-backend-agent/blob/main/steps/FEAT-ZD-48600/BE-02/README.md).

---
**2026-10-25 21:04:57**

⏸ **Gate DE-02 Access to secrets** needs **Data engineer**. Review [task.secrets_scope](https://github.com/arghya05/hobasa-data-engineering-agent/blob/main/outputs/FEAT-ZD-48600/task.secrets_scope.md) and the [step record](https://github.com/arghya05/hobasa-data-engineering-agent/blob/main/steps/FEAT-ZD-48600/DE-02/README.md) (checks and independent judge passed). Reply `/approve DE-02 Data engineer scores=c,c,g,u <comment>` or `/reject DE-02 Data engineer: <reason>`. *(SIMULATED gate: an automated approver decides on measurable criteria.)*

---
**2026-10-25 21:04:58**

✅ **DE-02 Access to secrets** (Data Engineering agent): done. Outputs: [task.secrets_scope](https://github.com/arghya05/hobasa-data-engineering-agent/blob/main/outputs/FEAT-ZD-48600/task.secrets_scope.md). [Inputs, attempts, checks and judge](https://github.com/arghya05/hobasa-data-engineering-agent/blob/main/steps/FEAT-ZD-48600/DE-02/README.md). Decisions: Data engineer: approve by sim.data_engineer.

---
**2026-10-25 21:05:06**

✅ **DS-02 Access to secrets** (Data Science agent): done. Outputs: [task.secrets_scope](https://github.com/arghya05/hobasa-data-science-agent/blob/main/outputs/FEAT-ZD-48600/task.secrets_scope.md). [Inputs, attempts, checks and judge](https://github.com/arghya05/hobasa-data-science-agent/blob/main/steps/FEAT-ZD-48600/DS-02/README.md).

---
**2026-10-25 21:05:17**

⏸ **Gate BE-03 Database changes** needs **Developer**. Review [task.db_changes](https://github.com/arghya05/hobasa-backend-agent/blob/main/outputs/FEAT-ZD-48600/task.db_changes.md) and the [step record](https://github.com/arghya05/hobasa-backend-agent/blob/main/steps/FEAT-ZD-48600/BE-03/README.md) (checks and independent judge passed). Reply `/approve BE-03 Developer scores=c,c,g,u <comment>` or `/reject BE-03 Developer: <reason>`. *(SIMULATED gate: an automated approver decides on measurable criteria.)*

---
**2026-10-25 21:05:19**

✅ **BE-03 Database changes** (Backend agent): done. Outputs: [task.db_changes](https://github.com/arghya05/hobasa-backend-agent/blob/main/outputs/FEAT-ZD-48600/task.db_changes.md). [Inputs, attempts, checks and judge](https://github.com/arghya05/hobasa-backend-agent/blob/main/steps/FEAT-ZD-48600/BE-03/README.md). Decisions: Developer: approve by sim.developer.

---
**2026-10-25 21:06:29**

⏸ **Gate DE-03 Database changes** needs **Data engineer**. Review [task.db_changes](https://github.com/arghya05/hobasa-data-engineering-agent/blob/main/outputs/FEAT-ZD-48600/task.db_changes.md) and the [step record](https://github.com/arghya05/hobasa-data-engineering-agent/blob/main/steps/FEAT-ZD-48600/DE-03/README.md) (checks and independent judge passed). Reply `/approve DE-03 Data engineer scores=c,c,g,u <comment>` or `/reject DE-03 Data engineer: <reason>`. *(SIMULATED gate: an automated approver decides on measurable criteria.)*

---
**2026-10-25 21:06:31**

✅ **DE-03 Database changes** (Data Engineering agent): done. Outputs: [task.db_changes](https://github.com/arghya05/hobasa-data-engineering-agent/blob/main/outputs/FEAT-ZD-48600/task.db_changes.md). [Inputs, attempts, checks and judge](https://github.com/arghya05/hobasa-data-engineering-agent/blob/main/steps/FEAT-ZD-48600/DE-03/README.md). Decisions: Data engineer: approve by sim.data_engineer.

---
**2026-10-25 21:06:57**

⏸ **Gate DS-03 Database changes** needs **Developer**. Review [task.db_changes](https://github.com/arghya05/hobasa-data-science-agent/blob/main/outputs/FEAT-ZD-48600/task.db_changes.md) and the [step record](https://github.com/arghya05/hobasa-data-science-agent/blob/main/steps/FEAT-ZD-48600/DS-03/README.md) (checks and independent judge passed). Reply `/approve DS-03 Developer scores=c,c,g,u <comment>` or `/reject DS-03 Developer: <reason>`. *(SIMULATED gate: an automated approver decides on measurable criteria.)*

---
**2026-10-25 21:06:58**

✅ **DS-03 Database changes** (Data Science agent): done. Outputs: [task.db_changes](https://github.com/arghya05/hobasa-data-science-agent/blob/main/outputs/FEAT-ZD-48600/task.db_changes.md). [Inputs, attempts, checks and judge](https://github.com/arghya05/hobasa-data-science-agent/blob/main/steps/FEAT-ZD-48600/DS-03/README.md). Decisions: Developer: approve by sim.developer.

---
**2026-10-25 21:08:48**

✅ **FE-03 Identify the components/layers to be changed** (Frontend agent): done. Outputs: [task.components](https://github.com/arghya05/hobasa-frontend-agent/blob/main/outputs/FEAT-ZD-48600/task.components.md). [Inputs, attempts, checks and judge](https://github.com/arghya05/hobasa-frontend-agent/blob/main/steps/FEAT-ZD-48600/FE-03/README.md).

---
**2026-10-25 21:09:42**

⏸ **Gate DE-04 Identify the sources/pipelines to be changed (Ingestion) ⁵** needs **Data engineer**. Review [task.components](https://github.com/arghya05/hobasa-data-engineering-agent/blob/main/outputs/FEAT-ZD-48600/task.components.md) and the [step record](https://github.com/arghya05/hobasa-data-engineering-agent/blob/main/steps/FEAT-ZD-48600/DE-04/README.md) (checks and independent judge passed). Reply `/approve DE-04 Data engineer scores=c,c,g,u <comment>` or `/reject DE-04 Data engineer: <reason>`. *(SIMULATED gate: an automated approver decides on measurable criteria.)*

---
**2026-10-25 21:09:43**

✅ **DE-04 Identify the sources/pipelines to be changed (Ingestion) ⁵** (Data Engineering agent): done. Outputs: [task.components](https://github.com/arghya05/hobasa-data-engineering-agent/blob/main/outputs/FEAT-ZD-48600/task.components.md). [Inputs, attempts, checks and judge](https://github.com/arghya05/hobasa-data-engineering-agent/blob/main/steps/FEAT-ZD-48600/DE-04/README.md). Decisions: Data engineer: approve by sim.data_engineer.
