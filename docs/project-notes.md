# Project notes — Murshid Mini (Razan)

## Data
All data is **hand-written synthetic teaching fixtures** (no real people, IDs or records). See [`results/core/synthetic_data.json`](../results/core/synthetic_data.json).

- `service_directory` — the approved public answer in Arabic (`ar`) and English (`en`).
- `records` — fictional applications keyed by reference number (e.g. `REF-1001`), each with an `owner` (a demo user) and a `status`.

## Architecture

Input → input guard → rule-based ticket extraction → schema/business-rule validation → public mock answer OR read-only tool → output validation → response + minimal metrics.

Day 4 places an exact cache around **only the two known public FAQs**. Status requests, malformed tickets and guarded requests bypass it. The key includes question, language, model label, prompt version and directory version. Entries expire after 300 seconds. Cached entries store the answer and creation time, not record status or session data.

## Components

- `FakeClient.generate`: finite lookup, increments mock-call counter. Never calls an API.
- `ask`: Day 1 baseline with UUID, answer, model label and measured Python latency.
- `extract_ticket`: simple rules and regex; not general NLP.
- `validate_ticket`: exact keys, types, enumerations and missing-reference consistency.
- `check_status`: local lookup with ownership check. Does not mutate records.
- `route`: rejects cancellation, handles clarification, chooses public vs status path.
- `build_prompt`: exposes a versioned teaching template. The mock does not execute prompts.
- `guard_input`: limited length, example injection strings and a ten-digit pattern. Not a comprehensive security/privacy detector.
- `run_pipeline`: coordinates validation and execution.
- `evaluate`: ten fixed cases plus reasons; no network or model judge.
- `run_app`: safe public-cache wrapper and minimal measurements.

## Cache rules (Day 4)
- Only the two known public FAQs are cached; status requests, invalid tickets and guarded inputs always bypass the cache.
- Cache key = question + language + model label + prompt version + directory version. Entries expire after 300 s.
- Measured times are local Python time, not model inference. Token prices are invented for the arithmetic only; real external API spend is zero.

## Tests
- Day 3: ten fixed golden cases (valid, incomplete, out-of-scope, injection, unauthorized). Result: 10/10.
- Day 4: the same ten cases re-run as a regression after adding the cache. Result: 10/10.
- 10/10 on fixed examples is not a general reliability guarantee.

## Limitations
- `FakeClient` is a deterministic mock, not a language model.
- Guards are simple examples (length, a few injection strings, a ten-digit pattern), not complete security or privacy detection.
- Authorization is a small synthetic ownership fixture.
