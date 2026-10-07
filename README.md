# Sirchmunk V3: Budgeted Graph Evidence Selection

[中文说明](README.zh-CN.md) · [Results](docs/results.md) · [Algorithm and mathematics](docs/algorithm.md) · [Reproduction](docs/reproduction.md)

An experimental selector for finding connected source evidence within document and byte budgets, integrated with a pinned Sirchmunk **DEEP** workflow. The native process still performs model analysis, retrieval, synthesis and correction. This is an independent research project, not an official ModelScope release.

## Current evidence: two cohorts, 80 distinct questions

This release contains the latest baseline/V3 measurements and the earlier completed cohort. Private source-ID and normalized-question checks found no overlap. The combined table retains every planned question, including one unfinished V3 run scored zero for answers:

| All 80 planned questions | Adapted native DEEP | V3 |
|---|---:|---:|
| Answer EM | 40/80 (50.0%) | 42/80 (52.5%) |
| Answer F1 | 71.56% | 72.02% |
| Complete supporting source documents read | 43/80 (53.75%) | 57/80 (71.25%) |
| Input + output tokens, including unfinished run | 1,165,698 | 954,562 |
| Model requests | 676 | 640 |
| Mean query time | 82.22 s | 83.49 s |
| Known-token peak-price estimate | CNY 2.834766 | CNY 2.397362 |

V3 used **18.1% fewer tokens** and had two additional EM-correct answers, with slightly higher measured time. It won 4 questions and lost 2; exploratory exact paired McNemar `p=0.6875`. **Overall superiority is not established.** Prices are token peak-price estimates, not invoices.

The earlier cohort used 1,600 shared paragraphs; the latest used 4,000. They are not one homogeneous 80-question experiment. The same completed baseline/V3 pairs total **79** questions, with EM `40/79` versus `42/79`; their costs exclude both rows of the unfinished pair. Both denominators and both cohorts remain available.

Latest cohort alone: all planned 40 questions have EM `19/40` versus `20/40`; the 39 completed pairs have EM `19/39` versus `20/39`, source completeness `20/39` versus `28/39`, 17.3% fewer V3 tokens and 1.2% higher V3 query time. Complete source coverage does not prove that evidence supports the answer.

![Baseline and V3: cohorts and combined results](docs/figures/v3_comparison.png)

## What is released

- V3's bounded title-connection candidate selector and native selection hook.
- Required shared delivery/snapshot adapters, authored fictional fixtures and offline tests.
- Two baseline/V3 cohorts: **160 pseudonymous scalar measurement rows**, aggregates, configuration and source hashes.
- Every V3 error and budget interruption in those exported rows; a separate retrieval diagnostic with a V3 regression.
- Mathematical definition, pseudocode, interpretation limits, scoring and statistics reproduction.

Only the baseline and V3 result rows are exported from wider registered studies. Other experimental implementations and result arms are outside this release. Internal shared V2 modules are dependencies rather than extra public experiment arms. The native and V3 results use the same shared answer-delivery layer.

## Quick start

Core tests and statistics use Python **3.12+** and the standard library:

```sh
python -B tools/run_core_tests.py
python -B scripts/recompute_results.py --check
```

Minimal selector use:

```python
from reliable_evidence.budget_graph_v3 import select_budget_graph

documents = {
    "clinic.md": "Clinic\nThe clinic works with Beacon Laboratory.",
    "laboratory.md": "Beacon Laboratory\nThe laboratory developed the test.",
}
choice = select_budget_graph(
    "Which laboratory developed the clinic's test?",
    documents, ["clinic.md", "laboratory.md"],
    max_files=2, max_evidence_bytes=4096,
)
print(choice.selected_names, choice.diagnostics)
```

To exercise actual native adaptive mechanics using an **already prepared** pinned runtime and its compatible Python environment:

```sh
python -B tools/verify_runtime.py --project /path/to/prepared-runtime
python -B tools/offline_native_smoke.py --project /path/to/prepared-runtime
```

The native smoke uses fictional documents, actual local retrieval tools and a scripted offline model. It makes no provider calls, reads no key or ledger, and does not install dependencies or download models. It is not a reproduction of paid QA accuracy. See [reproduction](docs/reproduction.md) for exact prerequisites and boundaries.

## Fixed sources and interpretation

Upstream: [`b314e11fcea87cf8146b2844cf2f991208c021d9`](https://github.com/modelscope/sirchmunk/tree/b314e11fcea87cf8146b2844cf2f991208c021d9). Historical API model: `deepseek-flash`, thinking disabled, maximum 512 output tokens per request. Each question/arm starts a separate cold engine; the adaptive context within a question remains.

This is adapted native DEEP, not unmodified FAST, FullWiki, or the LENS paper's full evaluation. Raw source text and exact private sampling exclusions are excluded, so the archive supports algorithm/mechanism reproduction and independent statistical recomputation, not exact regeneration of historical API responses or a private invoice. See [limitations](docs/limitations.md).

## License and publication

Authored code and documentation retain the [MIT license](LICENSE). Upstream Sirchmunk is Apache 2.0; HotpotQA data and reference code have their own terms. See [third-party notices](THIRD_PARTY_NOTICES.md) and [references](docs/references.bib).

This archive contains no live paid CLI, inherited spending allowance, private SQLite ledger, account receipt, raw prompt/answer dataset, credential, personal local path, model cache or Git history. [Manual upload instructions](UPLOAD_TO_GITHUB.zh-CN.md) describe publishing only this reviewed release directory.
