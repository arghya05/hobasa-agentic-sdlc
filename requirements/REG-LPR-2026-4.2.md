---
id: REG-LPR-2026-4.2
channel: Regulatory changes
source: Synthetic sample regulation LPR-2026 (not a real law), section 4.2, page 12
received: 2026-10-23
expected_type: Compliance
expected_route: compliance
repos: ["ap_aging"]
status: open
org_overrides: {"org.regulatory_sources": "LPR-2026 (synthetic sample regulation for testing, not a real law). Section 4.2, page 12: a payable more than 60 days past its due date and unpaid shall be reported as Late; Late applies from day 61 after the due date; paid invoices are never Late. Owner: compliance SME.", "org.rule_catalogue": "Rule Engine catalogue for AP (sample): RULE-AGING-BUCKETS (days-past-due buckets, decision D-2026-031). No rule implements LPR-2026 section 4.2 yet."}
owner_answers: {"Compliance SME": "Late means unpaid and days past due greater than 60 (day 61 onward). Exactly 60 days is not Late. Report count and total amount of Late invoices."}
---
Update on named regulatory source LPR-2026 (synthetic sample regulation used for testing only), section 4.2, page 12: 'A payable that is more than 60 days past its due date and remains unpaid shall be reported as Late. The Late status applies from day 61 after the due date. Paid invoices are never Late.' The AP module must identify Late invoices and report their count and total amount.
