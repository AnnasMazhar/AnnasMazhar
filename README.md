# Annas Mazhar

Data engineer. I build data platforms on AWS and, outside work hours, small autonomous
systems and research tooling — mostly Python, always with a bias for things that can be
checked rather than believed.

**The rule I build to:** if a tool makes a claim, it should be able to prove it. Each repo
below ships the tests, an evidence file, and the failure modes it does *not* hide.

---

## Current work

### [factorproof](https://github.com/AnnasMazhar/factorproof) — factor research that refuses to promote noise
Purged walk-forward cross-validation with embargo, IC decay curves, Benjamini-Hochberg FDR
across the whole factor family, a deflated Sharpe ratio reported per factor (computed, not
gated) — and a promotion gate a factor must satisfy before it is allowed into a portfolio.

```console
$ factor-lab list
Name                   Category           Description
mom_20                 momentum           20-day log-return (short-term momentum)
rev_5                  reversal           Negated 5-day log-return (short-term reversal)
vol_20                 volatility         20-day realised volatility, annualised
rsi_14                 oscillator         14-day Relative Strength Index (Wilder smoothing)
```

[![CI](https://github.com/AnnasMazhar/factorproof/actions/workflows/ci.yml/badge.svg)](https://github.com/AnnasMazhar/factorproof/actions/workflows/ci.yml) MIT

### [replayproof](https://github.com/AnnasMazhar/replayproof) — offline regression testing for LLM agents
Record an agent run once, re-run it forever with **zero API keys**. Assert tool-call
contracts, gate the token cost of a change, and diff behaviour when you swap the model
underneath.

```console
$ agenteval replay --run examples/recordings/sample_run.jsonl --mode strict
$ agenteval drift  --baseline base_result.json --current new_result.json
```

[![CI](https://github.com/AnnasMazhar/replayproof/actions/workflows/ci.yml/badge.svg)](https://github.com/AnnasMazhar/replayproof/actions/workflows/ci.yml) MIT

### [fitsproof](https://github.com/AnnasMazhar/fitsproof) — local inference that proves it fits
A calibrated cost model and an enforced memory budget in front of a from-scratch NumPy
inference engine (KV cache, quantisation). When the model does not fit, it says so loudly
instead of OOM-ing silently at token 400.

```console
$ fitsproof probe
Probing machine...
  bandwidth:  6.69 GB/s
  gemm:       314.31 GFLOPS
  RAM:        33.55 GB
  VRAM:       0.00 GB
```

[![CI](https://github.com/AnnasMazhar/fitsproof/actions/workflows/ci.yml/badge.svg)](https://github.com/AnnasMazhar/fitsproof/actions/workflows/ci.yml) MIT

### warehouse-mcp — least-privilege SQL for agents *(not yet public)*
An MCP server that gives an AI agent read access to a warehouse through a SQL-AST-enforced
column policy, row filters, query budgets, redaction and an append-only audit trail.
*In progress.*

---

## Upstream contributions

Merged work in other people's repos. 17 PRs in total; these are the ones worth reading.

- [aws/aws-cdk#37815](https://github.com/aws/aws-cdk/pull/37815) — `fix(glue-alpha)`: restore `notifyDelayAfter` to PySpark and Scala Spark ETL jobs (13k★)
- [google/zx#1464](https://github.com/google/zx/pull/1464) — `fix(deps)`: skip `node:` protocol imports in `--install` (46k★)
- [teng-lin/notebooklm-py#2262](https://github.com/teng-lin/notebooklm-py/pull/2262) — `feat(mcp)`: `source_delete` accepts multiple sources (20k★)
- [strands-agents/harness-sdk#4067](https://github.com/strands-agents/harness-sdk/pull/4067), [#4059](https://github.com/strands-agents/harness-sdk/pull/4059), [#3955](https://github.com/strands-agents/harness-sdk/pull/3955) — dropped content blocks, context offloader, llama.cpp usage chunk (9.2k★)
- [dlt-hub/dlt#4283](https://github.com/dlt-hub/dlt/pull/4283), [#3928](https://github.com/dlt-hub/dlt/pull/3928) — table-prefix layout, decimal coercion (6.1k★)
- [Cygnux-Labs/Tracekit#474](https://github.com/Cygnux-Labs/Tracekit/pull/474), [exmergo/dex#775](https://github.com/exmergo/dex/pull/775), [ferrumio/pynox#40](https://github.com/ferrumio/pynox/pull/40)

Some of these went through review: `dex#775` got changes requested, then approved, and
`harness-sdk#4067` was approved by a maintainer.

---

## How these are built

Each repo went through the same iteration protocol — research → implement → evaluate →
adversarial review → mutation testing — with the evidence committed next to the code
(`EVIDENCE.md`, `docs/ADVERSARIAL_REVIEW.md`, `reports/`).

CI runs each suite on Python 3.11 and 3.12, plus `ruff check` and `ruff format --check`.
The badges above are live status, not a number I typed and forgot to update.

Where something is unfinished or wrong, the README says so. A repo that hides its gaps is a
demo; one that states them is a piece of work.

---

## Elsewhere

- AWS data lake engineering — Glue, Athena, S3, orchestration; cost and correctness at scale
- I keep forks of dbt, Dagster and Ibis for reading. They are not contributions.
