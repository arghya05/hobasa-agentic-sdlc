---
id: PROV-ACME-2026-11
channel: LLM provider changes
source: Provider deprecation notice (sample, synthetic): acme-llm, 2026-10-20
received: 2026-10-20
expected_type: Technical
expected_route: technical
repos: ["ap_forecast"]
status: open
org_overrides: {"org.model_dependency_map": "ap_forecast uses provider acme-llm model acme-text-2 (config src/ap_forecast/models.json) for the payment-delay explanation; no other feature uses acme-llm.", "org.architecture": "ap_forecast is a Python 3.9 library: predict_delay_days(history) and build_explanation_request(vendor, predicted_days, config=None) returning {provider, model, max_tokens, messages}; the model comes from models.json. Keep both function signatures."}
---
Provider notice from acme-llm: model 'acme-text-2' is deprecated on 2026-12-01. Replace it with 'acme-text-3'. The new model requires a 'system' field (a string) in every request and accepts max_tokens up to 4096. Our explanation requests must keep max_tokens at 300 and add the system text 'You explain AP payment forecasts in one plain sentence.'
