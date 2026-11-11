# Submission notes

The entry point is `solution.py:build()` and implements the supplied `ingest`, `answer`, and `conflicts` contract. It uses only Python's standard library; no API keys, external downloads, model services, or network access are needed.

Each crawl is retained as a dated, complete snapshot. Requests with `as_of` use the latest snapshot not later than that date. Queries without a date use the newest crawl. This avoids exposing later rates to historical requests.

For structured products, the solution parses markdown tables and selects rates by product type, term, model year, balance tier, and whether the request is for APY or APR. Direct, authoritative product tables take precedence over archived marketing and calculator pages. For unstructured questions, it retrieves source excerpts using term overlap, matching page titles, and page-authority weighting. The answer carries the URL and crawl identifier of the supporting page. Where the supplied pages do not state a requested rate, it declines to invent one. All responses are deterministic, and answer calls require no model inference.

`conflicts()` compares the same product and tier across dated official tables, returns competing observed percentages with evidence, and resolves to the newest published table. Different terms and balance tiers are deliberately treated as different facts, not contradictions. The approach prioritizes reproducibility and fast response times over unsupported generative synthesis; highly unstructured questions can be less complete than structured rate questions.

Run from the **original kit root** (where `harness/`, `eval/`, and `snapshots_zip/` live):

```bash
python harness/run_eval.py --submission submission --eval eval/public_eval.jsonl
```

The participant ZIP intentionally contains only submission code and notes. The original website snapshots remain in the organizer-provided kit and are consumed by the harness at runtime; they are not redistributed here.
