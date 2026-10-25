# Journey FEAT-ZD-48600

**Requirement:** AP managers want to see which overdue invoices belong to vendors that usually pay late, so they can chase them first. (1) Data engineering, ap_pipeline: the vendor feed gains an optional paid_date column (ISO date, empty when unpaid); an invalid paid_date rejects the row with reason 'paid_date'; add delays_by_vendor(records) returning {vendor: [delay_days, ...]} for paid records with a paid_date, where delay_days = (paid_date - due_date) in days, in feed order. (2) AI / data science, ap_forecast: add vendor_risk(history) returning 'high' when predict_delay_days(history) > 30, 'medium' when it   
**Source:** Zendesk ticket ZD-48600 (sample, synthetic) (Customer Feedback) · **classified:** — · **fitment:** — · **route:** — · **repositories:** ap_aging, ap_forecast, ap_pipeline, ap_portal  
**Gates:** SIMULATED (automated test) · updated 2026-10-25 11:30

Every agent reads this board at session start. Approved outputs below are readable with context_get and cited as journey:<item>. Legend: ✓ done · ▶ running · ⏸ waiting for a person · ? waiting for an owner answer · ✓↻ done, an input it read was updated later · 🔎 ran as a check (condition not met, nothing changed) · – skipped · ✗ stopped · · next

## Execution map (who works first, what runs in sequence, what runs in parallel)

1. **In sequence:** ✓ REQ-01 → ✓ REQ-02 → · REQ-03
2. **In sequence:** (route set by the Grouping category and fitment)

## Done so far (newest last)

| # | Step | Agent | Outputs in GitHub | Approach and summary | Human decision | Judge | Attempts |
|---|---|---|---|---|---|---|---|
| 1 | REQ-01 Requirement Intake | Requirement | [feat.intake](https://github.com/arghya05/hobasa-requirement-agent/blob/main/outputs/FEAT-ZD-48600/feat.intake.md), [feat.prebacklog](https://github.com/arghya05/hobasa-requirement-agent/blob/main/outputs/FEAT-ZD-48600/feat.prebacklog.md) · [step record](https://github.com/arghya05/hobasa-requirement-agent/blob/main/steps/FEAT-ZD-48600/REQ-01/README.md) | Attempt 3 fixes the one refusal reason. A-2 said amounts were formatted to two decimals "only when rendered". That contradicted the architecture override in requirements/ZD-48600.md, which says JSON between services carries amounts as strings with two decimals.  A-2 now follows the sources. Inside ap_aging the amount is the Invoice amount (Decimal, 2 dp). It travels to ap_portal as a two-decimal s | PM: approve by sim.pm | scores {'correct': 5, 'complete': 4, 'grounded': 5, 'useful': 5} | 3 |
| 2 | REQ-02 Grouping | Requirement | [feat.classification](https://github.com/arghya05/hobasa-requirement-agent/blob/main/outputs/FEAT-ZD-48600/feat.classification.md) · [step record](https://github.com/arghya05/hobasa-requirement-agent/blob/main/steps/FEAT-ZD-48600/REQ-02/README.md) | This attempt fixes the G1 refusal. FIN-OPS-2026-07 had been listed among the related items said to share a rule or code with ZD-48600. It is a configuration-only change to max_tokens and shares neither, so I removed it from the grouped list and marked it "Not grouped" in the duplicate table. Its max_tokens conflict with PROV-ACME-2026-11 is kept only as a side observation for the PM (new OQ-5), sp | PM: approve by sim.pm | scores {'correct': 5, 'complete': 5, 'grounded': 5, 'useful': 5} | 5 |
