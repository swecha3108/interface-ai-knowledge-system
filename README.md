# Versioned Knowledge System — Hackathon Submission

A deterministic, source-grounded Python solution using only the supplied snapshots.

## Contents

- `solution.py` — required `build()` entry point; `ingest`, `answer`, and `conflicts` implementation.
- `requirements.txt` — no third-party dependencies.
- `NOTES.md` — approach, source ranking, historical handling, limitations, and API-key policy.

## Evaluate

Unzip the organizer-provided participant kit. Place this `submission` directory at the kit root next to `harness`, `eval`, and `snapshots_zip`.

```bash
python harness/run_eval.py --submission submission --eval eval/public_eval.jsonl
```

Optional built-in contract self-test:

```bash
python harness/run_eval.py --submission submission --snapshots harness/selftest/snapshots --eval harness/selftest/eval.jsonl --conflicts-gold harness/selftest/conflicts_gold.json
```

The code works with Python 3.9+ and does not make network requests or require tokens.

## Results verified locally

- 40-question public practice score (without conflict gold): **0.9620**.
- Bundled 5-question self-test with conflict gold: **1.0000**.
- Zero evaluation errors or stale-trap hits on the public practice set.

These are results on visible tests only. The unknown private benchmark may differ. Do not add answer keys or organizer datasets to your submission repository.
