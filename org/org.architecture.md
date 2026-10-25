# org.architecture

ap_aging is a pure Python 3.9 library (src/ap_aging) used by the AP API. Public functions: aging_buckets(invoices, as_of), days_past_due(due_date, as_of), bucket_for(days). Invoices are dicts with id, due_date (date), amount (Decimal), paid (bool). No database, no network, no secrets. Backward compatibility: existing function signatures and return shapes must not change.
