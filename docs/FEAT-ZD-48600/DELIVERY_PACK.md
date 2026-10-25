# Delivery pack FEAT-ZD-48600

AP managers want to see which overdue invoices belong to vendors that usually pay late, so they can chase them first. (1) Data engineering, ap_pipeline: the vendor feed gains an optional paid_date column (ISO date, empty when unpaid); an invalid paid_date rejects the row with reason 'paid_date'; add delays_by_vendor(records) returning {vendor: [delay_days, ...]} for paid records with a paid_date, where delay_days = (paid_date - due_date) in days, in feed order. (2) AI / data science, ap_forecast: add vendor_risk(history) returning 'high' when predict_delay_days(history) > 30, 'medium' when it is > 10, otherwise 'low'; build_explanation_request gains an optional risk argument and, when given, the prompt ends with ' Risk level: <risk>.'. (3) Backend, ap_aging: add overdue_with_risk(invoices, as_of, risk_by_vendor) returning, for unpaid invoices more than 30 days past due, a list of {'id', 'vendor', 'days', 'amount', 'risk'} sorted by days descending then id, with risk 'unknown' for vendors not in risk_by_vendor. (4) Frontend, ap_portal: add renderOverdueRisk(rows) rendering '<table class="overdue-risk">' with one '<tr class="risk-RISK">' per row showing id, vendor, days and amount to two decimals, and an empty string when there are no rows. The whole flow must be proven end to end: feed -> delays -> risk -> overdue list -> portal table.

## REQ-01 Requirement Intake (Requirement agent): feat.intake

# feat.intake: FEAT-ZD-48600

| Field | Value | Source |
|---|---|---|
| Trace ID | FEAT-ZD-48600 | record:brief |
| Channel | Customer Feedback | record:intake |
| Source | Zendesk ticket ZD-48600 (sample, synthetic) | record:intake |
| Received | 2026-10-24 | record:intake |
| Source link (GitHub) | `hobasa-agentic-sdlc/requirements/ZD-48600.md` | record:intake; file:hobasa-agentic-sdlc/requirements/ZD-48600.md |
| Repositories named in the source file | ap_pipeline, ap_forecast, ap_aging, ap_portal | file:hobasa-agentic-sdlc/requirements/ZD-48600.md |

## Original intake text (verbatim, treated as data)

> AP managers want to see which overdue invoices belong to vendors that usually pay late, so they can chase them first. (1) Data engineering, ap_pipeline: the vendor feed gains an optional paid_date column (ISO date, empty when unpaid); an invalid paid_date rejects the row with reason 'paid_date'; add delays_by_vendor(records) returning {vendor: [delay_days, ...]} for paid records with a paid_date, where delay_days = (paid_date - due_date) in days, in feed order. (2) AI / data science, ap_forecast: add vendor_risk(history) returning 'high' when predict_delay_days(history) > 30, 'medium' when it is > 10, otherwise 'low'; build_explanation_request gains an optional risk argument and, when given, the prompt ends with ' Risk level: <risk>.'. (3) Backend, ap_aging: add overdue_with_risk(invoices, as_of, risk_by_vendor) returning, for unpaid invoices more than 30 days past due, a list of {'id', 'vendor', 'days', 'amount', 'risk'} sorted by days descending then id, with risk 'unknown' for vendors not in risk_by_vendor. (4) Frontend, ap_portal: add renderOverdueRisk(rows) rendering '<table class="overdue-risk">' with one '<tr class="risk-RISK">' per row showing id, vendor, days and amount to two decimals, and an empty string when there are no rows. The whole flow must be proven end to end: feed -> delays -> risk -> overdue list -> portal table.

Source: record:intake; file:hobasa-agentic-sdlc/requirements/ZD-48600.md

## Extracted change requests

These are faithful splits of the text above. No facts have been added.

| ID | Area / repository (as named in the ticket) | Change requested |
|---|---|---|
| CR-0 | Business need | AP managers can see which overdue invoices belong to vendors that usually pay late, so they can chase them first. |
| CR-1 | Data engineering / ap_pipeline | The vendor feed gains an optional `paid_date` column (ISO date, empty when unpaid). An invalid `paid_date` rejects the row with reason `'paid_date'`. |
| CR-2 | Data engineering / ap_pipeline | New `delays_by_vendor(records)` returns `{vendor: [delay_days, ...]}` for paid records with a `paid_date`, where `delay_days = (paid_date - due_date)` in days, in feed order. |
| CR-3 | AI / data science / ap_forecast | New `vendor_risk(history)` returns `'high'` when `predict_delay_days(history) > 30`, `'medium'` when it is `> 10`, and `'low'` otherwise. |
| CR-4 | AI / data science / ap_forecast | `build_explanation_request` gains an optional `risk` argument. When `risk` is given, the prompt ends with `' Risk level: <risk>.'`. |
| CR-5 | Backend / ap_aging | New `overdue_with_risk(invoices, as_of, risk_by_vendor)`. For unpaid invoices more than 30 days past due, it returns a list of `{'id', 'vendor', 'days', 'amount', 'risk'}`, sorted by days descending and then by id. A vendor not in `risk_by_vendor` gets risk `'unknown'`. |
| CR-6 | Frontend / ap_portal | New `renderOverdueRisk(rows)` renders `<table class="overdue-risk">` with one `<tr class="risk-RISK">` per row. Each row shows id, vendor, days and amount (amount to two decimals). It returns an empty string when there are no rows. |
| CR-7 | Cross-repository | The whole flow must be proven end to end: feed -> delays -> risk -> overdue list -> portal table. |

Source for every row: record:intake


## REQ-01 Requirement Intake (Requirement agent): feat.prebacklog

# feat.prebacklog: FEAT-ZD-48600

**Pre Backlog entry, status: Draft for PM review.** This step does not approve or prioritize anything.

## 1. Entry

| Field | Value | Source |
|---|---|---|
| Trace ID | FEAT-ZD-48600 | record:brief |
| Title | Overdue invoices ranked by vendor late-payment risk (feed -> delays -> risk -> overdue list -> portal table) | record:intake |
| Intake | Zendesk ticket ZD-48600 (sample, synthetic), Customer Feedback, received 2026-10-24 | record:intake |
| Source link | `hobasa-agentic-sdlc/requirements/ZD-48600.md` (full intake in feat.intake) | record:intake; file:hobasa-agentic-sdlc/requirements/ZD-48600.md |
| Business need | AP managers want to see which overdue invoices belong to vendors that usually pay late, so they can chase them first. | record:intake |
| Linked roadmap item | **R-AP-12**, "give AP managers earlier visibility of overdue payables" (Q4 2026 roadmap, AP module, owner PM) | org.roadmap |
| Not linked | R-AP-14, "aging export for finance close". The ticket asks for no export. | org.roadmap; record:intake |
| Affected components | ap_pipeline (CR-1, CR-2), ap_forecast (CR-3, CR-4), ap_aging (CR-5), ap_portal (CR-6), plus an end-to-end proof across all four (CR-7) | record:intake |
| Routing named in the source file | ap_pipeline -> Data Engineering Coding Agent; ap_forecast -> Data Science Agent; ap_aging -> Backend Coding Agent; ap_portal -> Frontend Coding Agent; integration and end-to-end tests across all four -> Testing Agent | file:hobasa-agentic-sdlc/requirements/ZD-48600.md |
| Item type stated in the source file | New Feature | file:hobasa-agentic-sdlc/requirements/ZD-48600.md |
| Risk note in the source file | No finance posting, authentication, tenancy or payment execution; tier T2; the risk label is advisory only | file:hobasa-agentic-sdlc/requirements/ZD-48600.md |
| Owner | PM | org.roadmap |

## 2. Intake checks

| Check (workbook action) | Result | Source |
|---|---|---|
| Read the roadmap item and match it to planned work | The item matches R-AP-12. The ticket's goal (seeing overdue invoices so they can be chased first) falls under "earlier visibility of overdue payables". | org.roadmap; record:intake |
| Check against the Pre Backlog sheet and the DevOps board | **Not possible.** Neither the sheet nor the board was in this step's context. As a substitute I read the related requirement files in the repository. No duplicate was found, but there are three related open items (section 3). | record:brief; file:hobasa-agentic-sdlc/requirements/ZD-48211.md; file:hobasa-agentic-sdlc/requirements/ZD-48455.md; file:hobasa-agentic-sdlc/requirements/ZD-48501.md |
| Check the decision for conflict with prior decisions | No conflict found (section 4). | org.decision_log; record:memory |
| Match the change against the connector inventory | **ap_aging (CR-5):** the inventory states that no source-system connector is affected by the ap_aging library. **ap_pipeline, ap_forecast, ap_portal (CR-1 to CR-4, CR-6):** the inventory says nothing about these repositories, so this step cannot confirm whether any connector is affected. CR-1 changes the vendor feed (a new optional `paid_date` column). The source file records this as vendor feed v3, with the daily 02:00 Asia/Kolkata schedule unchanged. Whether that counts as a connector change is open (OQ-3). | org.connector_inventory; record:intake; file:hobasa-agentic-sdlc/requirements/ZD-48600.md |
| Capture regulatory section and page, and the rules affected | Not applicable. No regulatory source applies to this change, so there is no section or page to cite and no rule is changed or added. | org.regulatory_sources |
| Match the change against the model dependency map | ap_forecast uses provider acme-llm, model acme-text-2 (config `src/ap_forecast/models.json`), for the payment-delay explanation. CR-4 changes the prompt of the explanation request, so the feature depends on this model. `vendor_risk` (CR-3) uses no LLM; it is a rule on the predicted delay. The ticket does not mention any change of provider or model. | org.model_dependency_map; record:intake |
| Gather external patterns and cite each source | Not applicable. This is a customer ticket and no market or competitive input was part of the trigger. | record:intake |
| Transcript / meeting gateways | Not applicable. The channel is Customer Feedback (a ticket), not a meeting transcript. | record:intake |

## 3. Related open requirements (possible overlap)

These are not duplicates, but should be considered together when the entry is grouped.

| File | Received / status / repositories | Overlap with this entry | Source |
|---|---|---|---|
| `requirements/ZD-48211.md` | 2026-10-20; open; ap_aging | Asks to flag every open invoice more than 30 days past its due date as overdue, and to add an overdue summary (number of overdue invoices and their total amount). Paid invoices never count as overdue. CR-5 in this entry uses the same overdue rule. | file:hobasa-agentic-sdlc/requirements/ZD-48211.md |
| `requirements/ZD-48501.md` | 2026-10-24; open; ap_aging, ap_portal | Adds `overdue_summary(invoices, as_of)` returning `{'count': int, 'total': Decimal}` for unpaid invoices more than 30 days past due, plus a `badge-overdue` portal badge. Same overdue rule and the same `as_of` parameter style as CR-5; different function and view. | file:hobasa-agentic-sdlc/requirements/ZD-48501.md |
| `requirements/ZD-48455.md` | 2026-10-22; open; ap_portal | Highlights the 61-90 and 'Over 90 days' aging rows as overdue risk (CSS class `row-overdue`) and adds a total row. The name is similar to this entry's `overdue-risk` table and `risk-*` row classes, but it is a different view (the aging summary table). | file:hobasa-agentic-sdlc/requirements/ZD-48455.md |

Comparison against this entry: record:intake

## 4. Decision log and lessons check

| Item | Bearing on this entry | Conflict? | Source |
|---|---|---|---|
| D-2026-031: aging buckets use calendar days after due date | Applies to CR-5 "days past due". I assume the overdue count also uses calendar days (A-1). The decision covers aging buckets only, so it does not settle the day unit for `delay_days` in CR-2 (OQ-2). | No | org.decision_log; record:intake |
| D-2026-044: monetary amounts use Decimal, never float | CR-5 `amount` must stay Decimal. Per the source file, JSON between services carries amounts as strings with two decimals; CR-6 shows them to two decimals. | No | org.decision_log; record:intake; file:hobasa-agentic-sdlc/requirements/ZD-48600.md |
| D-2026-050: paid invoices are excluded from aging | CR-5 covers unpaid invoices only, which is consistent. CR-2 uses paid records only for delay history, not for aging. | No | org.decision_log; record:intake |
| L-007: test the boundary day (exactly 30 days) explicitly | Boundaries to test: exactly 30 days past due (CR-5, `> 30`), and predicted delay of exactly 30 and exactly 10 (CR-3, `> 30` / `> 10`). | n/a | record:memory; record:intake |
| L-011: keep Decimal arithmetic; never convert amounts to float | Applies to amounts carried through CR-5 and CR-7. | n/a | record:memory |

## 5. Assumptions (non-blocking)

- **A-1:** "days past due" in CR-5 means calendar days after the due date, in line with D-2026-031. (org.decision_log)
- **A-2:** `delay_days` in CR-2 can be zero or negative when a vendor paid on or before the due date. Such values are kept in feed order. (record:intake; see OQ-2)
- **A-3:** `risk_by_vendor` (CR-5) is built from `vendor_risk` (CR-3) applied to each vendor's `delays_by_vendor` history (CR-2). This follows from the flow named in CR-7. (record:intake)
- **A-4:** The `RISK` placeholder in `<tr class="risk-RISK">` (CR-6) is the risk value of the row: high, medium, low or unknown. The source file names the classes `risk-high`, `risk-medium`, `risk-low` and `risk-unknown`. (record:intake; file:hobasa-agentic-sdlc/requirements/ZD-48600.md)

## 6. Open questions (non-blocking)

- **OQ-1:** The Pre Backlog sheet and the DevOps board were not available, so the duplicate check covered only the repository's requirement files. PM: please confirm there is no existing entry for this need.
- **OQ-2:** Is the day unit for `delay_days` (CR-2) calendar days, and should early payments (zero or negative delay) be included? D-2026-031 covers aging buckets only.
- **OQ-3:** The connector inventory covers only ap_aging. Is any source-system connector affected by the ap_pipeline vendor-feed change (the new `paid_date` column, CR-1), or by the ap_forecast or ap_portal changes? Should the feed change be recorded in the connector inventory?
- **OQ-4:** How should a row be handled if `paid` and `paid_date` disagree (for example, paid with an empty `paid_date`, or unpaid with a date)? The ticket defines only the invalid-date rejection.
- **OQ-5:** What should `vendor_risk` return for a vendor with an empty history? This depends on how `predict_delay_days` behaves today, which this step did not read.
- **OQ-6:** Should vendor names and ids be HTML-escaped in `renderOverdueRisk` (CR-6)? The ticket does not say.
- **OQ-7:** Should this entry be grouped with, or sequenced after, the related open items ZD-48211 and ZD-48501, which share the same overdue rule (unpaid, more than 30 days past due)?

## 7. Notification

This step sent no notification. This entry is the notification content for the PM gate on FEAT-ZD-48600. Sending it is left to the workflow after evaluation. (record:brief)


## REQ-02 Grouping (Requirement agent): feat.classification

# feat.classification: FEAT-ZD-48600

**Grouping result, status: Draft for sampled human evaluation.** This step classifies the entry and checks for duplicates. It does not approve, prioritize or create a ticket in an external system. The record below is the content of the new ticket. (record:brief)

## 1. Classification

| Field | Value | Source |
|---|---|---|
| Trace ID | FEAT-ZD-48600 | record:brief |
| Pre Backlog entry | Overdue invoices ranked by vendor late-payment risk (feed -> delays -> risk -> overdue list -> portal table), linked to roadmap item R-AP-12 | feat.prebacklog |
| **Category** | **New Feature** | file:hobasa-agentic-sdlc/requirements/ZD-48600.md; feat.prebacklog |
| Why this category | The source file records the item type as New Feature. The ticket asks for new functions (`delays_by_vendor`, `vendor_risk`, `overdue_with_risk`, `renderOverdueRisk`), a new optional feed column and a new optional argument. The architecture says to keep every existing signature and add new functions. feat.prebacklog records that no regulatory source applies. | file:hobasa-agentic-sdlc/requirements/ZD-48600.md; feat.intake; org.architecture; feat.prebacklog |
| **Qualifier** | **Not Technical Only** | feat.intake |
| Why this qualifier | The business need is that AP managers can see which overdue invoices belong to vendors that usually pay late. CR-6 adds a new portal table (`renderOverdueRisk`) for this. RETRO-2026-19 uses "Technical only" for an item with "no customer-visible change". This entry does not fit that description. | feat.intake; file:hobasa-agentic-sdlc/requirements/RETRO-2026-19.md |
| Route named in the source file | full | file:hobasa-agentic-sdlc/requirements/ZD-48600.md |
| Risk note in the source file | No finance posting, authentication, tenancy or payment execution; tier T2; the risk label is advisory only | file:hobasa-agentic-sdlc/requirements/ZD-48600.md; feat.prebacklog |

## 2. Technical sub-categories (one per change request)

The trigger asks for a technical sub-category under each entry. Each change request below is a technical sub-item of this New Feature, grouped by the area the ticket names and routed by the feature routing map.

| CR | Technical sub-category (area named in the ticket) | Repository | Owner agent (routing map) | Source |
|---|---|---|---|---|
| CR-1 | Data engineering: optional `paid_date` feed column; invalid `paid_date` rejects the row with reason `'paid_date'` | ap_pipeline | Data Engineering Coding Agent | feat.intake; org.routing_map |
| CR-2 | Data engineering: new `delays_by_vendor(records)` | ap_pipeline | Data Engineering Coding Agent | feat.intake; org.routing_map |
| CR-3 | AI / data science: new `vendor_risk(history)`, a rule on the predicted delay (no LLM) | ap_forecast | Data Science Agent | feat.intake; feat.prebacklog; org.routing_map |
| CR-4 | AI / data science: optional `risk` argument on `build_explanation_request` (prompt of the payment-delay explanation; depends on acme-llm, acme-text-2) | ap_forecast | Data Science Agent | feat.intake; feat.prebacklog; org.routing_map |
| CR-5 | Backend: new `overdue_with_risk(invoices, as_of, risk_by_vendor)` | ap_aging | Backend Coding Agent | feat.intake; org.routing_map |
| CR-6 | Frontend: new `renderOverdueRisk(rows)` portal table | ap_portal | Frontend Coding Agent | feat.intake; org.routing_map |
| CR-7 | Integration and end-to-end tests across all four repositories | all four | Testing Agent | feat.intake; org.routing_map |

Impacted repositories: ap_pipeline, ap_forecast, ap_aging, ap_portal

Basis: the feature routing map routes ap_pipeline, ap_forecast, ap_aging and ap_portal to their coding agents and routes the end-to-end tests across all four to the Testing Agent (org.routing_map). The ticket asks for a change in each of them (feat.intake). The organisation-level routing map lists only ap_aging (file:hobasa-agentic-sdlc/org/org.routing_map.md). The feature override covers the other three.

## 3. Duplicate check and merge decision

**No duplicates found. Nothing was merged.** I compared the entry with every requirement file in `hobasa-agentic-sdlc/requirements/`. The Pre Backlog sheet and the DevOps board were not in this step's context (OQ-1 in feat.prebacklog stays open).

| Item | Category in its file | Overlap with FEAT-ZD-48600 | Decision | Source |
|---|---|---|---|---|
| ZD-48211 | New Feature (ap_aging) | Same overdue rule as CR-5: open invoices more than 30 days past due; paid invoices never count as overdue. It asks for an overdue flag and an overdue summary (count and total amount), not a list with vendor risk. | **Related, not a duplicate. Keep separate.** | file:hobasa-agentic-sdlc/requirements/ZD-48211.md; feat.intake |
| ZD-48501 | New Feature (ap_aging, ap_portal) | Same overdue rule and the same `as_of` parameter as CR-5. It adds `overdue_summary` and a `badge-overdue` portal badge, which are a different function and a different view. | **Related, not a duplicate. Keep separate.** | file:hobasa-agentic-sdlc/requirements/ZD-48501.md; feat.intake |
| ZD-48470 | Enhancement (ap_pipeline) | Both change the vendor feed in ap_pipeline and both add a row rejection. ZD-48470 adds `currency` (feed v2, reason `'InvalidCurrency'`). This entry adds `paid_date` (feed v3, reason `'paid_date'`). | **Related, not a duplicate. Sequencing question (OQ-B).** | file:hobasa-agentic-sdlc/requirements/ZD-48470.md; file:hobasa-agentic-sdlc/requirements/ZD-48600.md; feat.intake |
| PROV-ACME-2026-11 | Technical (ap_forecast) | Replaces model acme-text-2 with acme-text-3 and adds a `system` field to the explanation requests. CR-4 changes the prompt built by `build_explanation_request`. | **Related, not a duplicate. Sequencing question (OQ-C).** | file:hobasa-agentic-sdlc/requirements/PROV-ACME-2026-11.md; feat.intake |
| ZD-48377 | Defect (ap_aging) | An invoice exactly 30 days past due lands in the 31-60 bucket instead of 1-30. CR-5 uses the same boundary (more than 30 days past due), and L-007 says to test that boundary explicitly. The defect file does not say whether the fault is in the day count or in the bucket mapping. | **Related, not a duplicate. Sequencing question (OQ-D).** | file:hobasa-agentic-sdlc/requirements/ZD-48377.md; feat.intake; record:memory |
| ZD-48455 | Enhancement (ap_portal) | A different view (the aging summary table, class `row-overdue`). Only the naming is similar. | Not a duplicate. | file:hobasa-agentic-sdlc/requirements/ZD-48455.md; feat.prebacklog |
| FIN-OPS-2026-07 | Configuration (ap_forecast) | Changes only the explanation `max_tokens`. The ZD-48600 ticket does not mention `max_tokens`. | Not a duplicate. | file:hobasa-agentic-sdlc/requirements/FIN-OPS-2026-07.md; feat.intake |
| REG-LPR-2026-4.2 | Compliance (ap_aging) | A "Late" rule for invoices more than 60 days past due. Different threshold and purpose. | Not a duplicate. | file:hobasa-agentic-sdlc/requirements/REG-LPR-2026-4.2.md |
| ZD-48480, ZD-48510, RETRO-2026-19 | Documentation, New Feature (vendor payment execution), Technical | They share only the repository (ap_aging). They do not ask for any of the functions or views in this entry. | Not duplicates. | file:hobasa-agentic-sdlc/requirements/ZD-48480.md; file:hobasa-agentic-sdlc/requirements/ZD-48510.md; file:hobasa-agentic-sdlc/requirements/RETRO-2026-19.md; feat.intake |

## 4. Decision log check

No classification here conflicts with D-2026-031, D-2026-044 or D-2026-050. feat.prebacklog recorded these as no conflict, and this step adds no new rule. (feat.prebacklog; record:memory)

## 5. Assumptions (non-blocking)

- **G-1:** "Technical Only" is a qualifier for items with no customer-visible change, as RETRO-2026-19 uses it. Because this entry adds a portal table for AP managers (CR-6), the qualifier is not applied to the entry as a whole. Each change request is still listed as a technical sub-category in section 2. (record:brief; file:hobasa-agentic-sdlc/requirements/RETRO-2026-19.md; feat.intake)
- **G-2:** Related items are kept as separate entries, not merged, because each asks for a different function or view. (feat.intake; the requirement files cited in section 3)

## 6. Open questions (non-blocking)

- **OQ-A:** The overdue rule (unpaid, more than 30 days past due) appears in ZD-48211, ZD-48501 and CR-5. Should ap_aging have one shared overdue rule used by all three, and in which order should they be built? (Carries OQ-7 from feat.prebacklog forward.)
- **OQ-B:** ZD-48470 brings feed v2 (`currency`). This entry is recorded as feed v3 (`paid_date`), but the v3 column list in the ZD-48600 source file does not include `currency`. Should ZD-48470 land first, and should feed v3 include `currency`?
- **OQ-C:** PROV-ACME-2026-11 replaces acme-text-2 and adds a `system` field to the explanation requests, and CR-4 changes the prompt of the same request. Which change lands first, and should CR-4 be built against the new request shape?
- **OQ-D:** Should the ZD-48377 boundary fix land before CR-5, so that the exactly-30-days boundary in `overdue_with_risk` is tested against corrected boundary handling?
- **OQ-E:** Are any of the change requests besides CR-6 visible to users? For example, does the explanation prompt in CR-4 reach users? The inputs do not say. This does not change the entry-level qualifier.
- **OQ-F:** The Pre Backlog sheet and the DevOps board were not available, so the duplicate check covered only the repository's requirement files (same as OQ-1 in feat.prebacklog).


## REQ-03 Product Fitment Validation (Requirement agent): feat.fitment

# feat.fitment: FEAT-ZD-48600

**Product Fitment Validation, status: Draft for the PM and Leadership gate.** This step returns a recommended verdict with its evidence. It does not approve, prioritize or route the entry. PM and Leadership make the Yes or No decision. (record:brief)

## 1. Verdict

| Field | Value | Source |
|---|---|---|
| Trace ID | FEAT-ZD-48600 | record:brief |
| Entry | Overdue invoices ranked by vendor late-payment risk (feed -> delays -> risk -> overdue list -> portal table) | feat.classification |
| Category / qualifier | New Feature / Not Technical Only | feat.classification |
| **Recommended verdict** | **Yes**, based on the roadmap evidence in section 2. The capability check (section 3) shows only new additions and no replacement. Strategy fit (section 4) is not established by the inputs and is left to PM and Leadership (OQ-F1). | sections 2 to 4 below |
| **Reason code** | **FIT-YES-ROADMAP**: the entry is linked to a planned roadmap item. | org.roadmap; journey:feat.prebacklog |
| Linked roadmap item | R-AP-12, "give AP managers earlier visibility of overdue payables" (Q4 2026 roadmap, AP module, owner PM) | org.roadmap; feat.classification |

## 2. Roadmap fit: Yes

| Check | Finding | Source |
|---|---|---|
| Roadmap item text | R-AP-12: "give AP managers earlier visibility of overdue payables". | org.roadmap |
| Ticket's business need | "AP managers want to see which overdue invoices belong to vendors that usually pay late, so they can chase them first." | journey:feat.intake |
| Link recorded at intake | REQ-01 linked the entry to R-AP-12. It recorded that the ticket's goal (seeing overdue invoices so they can be chased first) falls under "earlier visibility of overdue payables". The PM approved that step. | journey:feat.prebacklog; feat.classification |
| What the entry adds for AP managers | CR-5 returns unpaid invoices more than 30 days past due with a risk label. CR-6 renders them in a new portal table (`renderOverdueRisk`). | journey:feat.intake; feat.classification |
| Other roadmap items | R-AP-14, "aging export for finance close", is not linked. The ticket asks for no export. | org.roadmap; journey:feat.prebacklog |

## 3. Capability check: adds to the documented capability, replaces nothing

| Check | Finding | Source |
|---|---|---|
| Documented capability | "ap_aging service computes aging buckets (current, 1-30, 31-60, 61-90, 90+) for open invoices." | org.strategy_capability |
| Change in ap_aging | CR-5 adds a new function, `overdue_with_risk(invoices, as_of, risk_by_vendor)`, for unpaid invoices more than 30 days past due. | journey:feat.intake; feat.classification |
| Existing behaviour | The architecture recorded for this item says: "Keep every existing signature; add new functions." | file:hobasa-agentic-sdlc/requirements/ZD-48600.md; feat.classification |
| Parts outside the documented capability | CR-1 and CR-2 (ap_pipeline), CR-3 and CR-4 (ap_forecast), and CR-6 (ap_portal). org.strategy_capability describes only the ap_aging service, so it has no capability text for these repositories (OQ-F2). | feat.classification; org.strategy_capability |
| Risk note recorded in the source file | No finance posting, authentication, tenancy or payment execution; tier T2; the risk label is advisory only. | feat.classification; file:hobasa-agentic-sdlc/requirements/ZD-48600.md |

## 4. Strategy check: not established by the inputs

| Strategy statement | What the inputs say about this entry | Source |
|---|---|---|
| "help finance teams pay on time and avoid late-payment penalties" | No input links this entry to paying on time or to late-payment penalties. The ticket's stated purpose is to see overdue invoices of "vendors that usually pay late, so they can chase them first". Whether that purpose serves this strategy is for PM and Leadership to judge (OQ-F1). | org.strategy_capability; journey:feat.intake |
| "auditability and traceability are core product promises" | The flow must be proven end to end (CR-7). The inputs do not say whether the risk label, or the delay history and predicted delay behind it, must be recorded for audit (OQ-F3). | org.strategy_capability; feat.classification |

## 5. Decision log check

No conflict found. D-2026-050 says paid invoices are excluded from aging. CR-5 covers unpaid invoices only. D-2026-031 and D-2026-044 were checked at intake with no conflict, and this step adds no new rule. (record:memory; journey:feat.prebacklog; feat.classification)

## 6. Assumptions (non-blocking)

- **F-1:** The roadmap item speaks of "overdue payables". The ticket speaks of "vendors that usually pay late" and asks to "chase them first". CR-2 computes delay as `paid_date - due_date`. The verdict assumes the ticket concerns the AP module's overdue invoices, as REQ-01 recorded when it linked the entry to R-AP-12. (org.roadmap; journey:feat.intake; journey:feat.prebacklog)
- **F-2:** No list of fitment reason codes was in this step's inputs. FIT-YES-ROADMAP is a descriptive code proposed here (OQ-F4). (record:brief)

## 7. Open questions (non-blocking)

- **OQ-F1 (PM / Leadership):** Does this entry serve the strategy "help finance teams pay on time and avoid late-payment penalties"? What do "vendors that usually pay late" and "chase them first" mean for an AP (payables) module? The inputs do not say.
- **OQ-F2 (PM / Leadership):** org.strategy_capability describes only the ap_aging service. If this entry is approved, should it be updated to cover ap_pipeline, ap_forecast and ap_portal, and a vendor risk capability?
- **OQ-F3 (Leadership):** The strategy names auditability and traceability as core product promises. Should the vendor risk label, and the delay history and predicted delay behind it, be recorded or explainable for audit? This could become a business rule in the BRD (REQ-04).
- **OQ-F4 (PM):** Is there an approved list of fitment reason codes? If so, which code should replace FIT-YES-ROADMAP?
- Carried forward from feat.classification. These do not affect the verdict:
  - OQ-A to OQ-D: sequencing with ZD-48211, ZD-48501, ZD-48470, PROV-ACME-2026-11 and ZD-48377.
  - OQ-F: the Pre Backlog sheet and the DevOps board were not available.

## 8. Notification

This step sent no notification. This file is the notification content for PM and Leadership to decide Yes or No on FEAT-ZD-48600. Sending it is left to the workflow after evaluation. (record:brief)

