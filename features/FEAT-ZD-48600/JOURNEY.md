# Journey FEAT-ZD-48600

**Requirement:** AP managers want to see which overdue invoices belong to vendors that usually pay late, so they can chase them first. (1) Data engineering, ap_pipeline: the vendor feed gains an optional paid_date column (ISO date, empty when unpaid); an invalid paid_date rejects the row with reason 'paid_date'; add delays_by_vendor(records) returning {vendor: [delay_days, ...]} for paid records with a paid_date, where delay_days = (paid_date - due_date) in days, in feed order. (2) AI / data science, ap_forecast: add vendor_risk(history) returning 'high' when predict_delay_days(history) > 30, 'medium' when it   
**Source:** Zendesk ticket ZD-48600 (sample, synthetic) (Customer Feedback) · **classified:** — · **fitment:** — · **route:** — · **repositories:** ap_aging, ap_forecast, ap_pipeline, ap_portal  
**Gates:** SIMULATED (automated test) · updated 2026-10-25 10:55

Every agent reads this board at session start. Approved outputs below are readable with context_get and cited as journey:<item>. Legend: ✓ done · ▶ running · ⏸ waiting for a person · ? waiting for an owner answer · ✓↻ done, an input it read was updated later · 🔎 ran as a check (condition not met, nothing changed) · – skipped · ✗ stopped · · next

## Execution map (who works first, what runs in sequence, what runs in parallel)

1. **In sequence:** ✓ REQ-01 → ✓ REQ-02 → · REQ-03
2. **In sequence:** (route set by the Grouping category and fitment)

## Done so far (newest last)

| # | Step | Agent | Outputs in GitHub | Approach and summary | Human decision | Judge | Attempts |
|---|---|---|---|---|---|---|---|
| 1 | REQ-01 Requirement Intake | Requirement | [feat.intake](https://github.com/arghya05/hobasa-requirement-agent/blob/main/outputs/FEAT-ZD-48600/feat.intake.md), [feat.prebacklog](https://github.com/arghya05/hobasa-requirement-agent/blob/main/outputs/FEAT-ZD-48600/feat.prebacklog.md) · [step record](https://github.com/arghya05/hobasa-requirement-agent/blob/main/steps/FEAT-ZD-48600/REQ-01/README.md) | Attempt 3 fixes the G1 refusal on the connector check. I removed the blanket sentence "No source-system connector is affected". The connector row in feat.prebacklog now matches what org.connector_inventory says: no connector is affected by the ap_aging library, and the inventory says nothing about ap_pipeline, ap_forecast or ap_portal. That gap is now open question OQ-3, which asks whether the CR- | PM: approve by sim.pm | scores {'correct': 5, 'complete': 4, 'grounded': 5, 'useful': 5} | 3 |
| 2 | REQ-02 Grouping | Requirement | [feat.classification](https://github.com/arghya05/hobasa-requirement-agent/blob/main/outputs/FEAT-ZD-48600/feat.classification.md) · [step record](https://github.com/arghya05/hobasa-requirement-agent/blob/main/steps/FEAT-ZD-48600/REQ-02/README.md) | Attempt 2 fixes both G1 refusals, and I rewrote feat.classification in full. (1) In the ZD-48470 overlap row I removed the inferred claim that both changes use the same transform.to_model reject path. The row now states only what the files say: both change the ap_pipeline vendor feed and both add a row rejection ('InvalidCurrency' in feed v2, 'paid_date' in feed v3). (2) I removed the sentence "On | PM: approve by sim.pm | scores {'correct': 5, 'complete': 4, 'grounded': 5, 'useful': 4} | 2 |
