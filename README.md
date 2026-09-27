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
across the whole factor family, deflated Sharpe for the number of trials actually run — and
a promotion gate a factor must satisfy before it is allowed into a portfolio.

```console
$ factor-lab list
Name                   Category           Description
mom_20                 momentum           20-day log-return (short-term momentum)
rev_5                  reversal           Negated 5-day log-return (short-term reversal)
vol_20                 volatility         20-day realised volatility, annualised
rsi_14                 oscillator         14-day Relative Strength Index (Wilder smoothing)
```

`107 tests` · MIT

### [replayproof](https://github.com/AnnasMazhar/replayproof) — offline regression testing for LLM agents
Record an agent run once, re-run it forever with **zero API keys**. Assert tool-call
contracts, gate the token cost of a change, and diff behaviour when you swap the model
underneath.

```console
$ agenteval replay --run examples/recordings/sample_run.jsonl --mode strict
$ agenteval drift  --baseline base_result.json --current new_result.json
```

`136 tests` · MIT

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

`148 tests` · MIT

### warehouse-mcp — least-privilege SQL for agents *(not yet public)*
An MCP server that gives an AI agent read access to a warehouse through a SQL-AST-enforced
column policy, row filters, query budgets, redaction and an append-only audit trail.
*In progress.*

---

## How these are built

Each repo went through the same iteration protocol — research → implement → evaluate →
adversarial review → mutation testing — with the evidence committed next to the code
(`EVIDENCE.md`, `docs/ADVERSARIAL_REVIEW.md`, `reports/`).

The test counts above are not self-reported. They come from a fresh clone, a clean
virtualenv, `pip install -e '.[dev]'`, `pytest` and `ruff` — the same commands in each
README — and run on CI for Python 3.11 and 3.12.

Where something is unfinished or wrong, the README says so. A repo that hides its gaps is a
demo; one that states them is a piece of work.

---

## Elsewhere

- AWS data lake engineering — Glue, Athena, S3, orchestration; cost and correctness at scale
- Data tooling: [dbt](https://github.com/AnnasMazhar/dbt), [Dagster](https://github.com/AnnasMazhar/dagster), [Ibis](https://github.com/AnnasMazhar/ibis)
- Open-source contributions to [strands-agents/harness-sdk](https://github.com/strands-agents/harness-sdk)
