<div align="center">

<img src="docs/assets/phantera-gift-banner.png" alt="rightsize, a gift from Phantera. Same quality. Fewer tokens." width="100%">

<br/>

<a href="#install-in-one-line"><img src="https://img.shields.io/badge/Install-one%20line-00d4ff?style=for-the-badge&labelColor=0b0f14" alt="Install"></a>
<a href="#measured-not-claimed"><img src="https://img.shields.io/badge/Up%20to-98%25%20cheaper-00d4ff?style=for-the-badge&labelColor=0b0f14" alt="Up to 98% cheaper"></a>
<img src="https://img.shields.io/badge/price-free%20forever-ffffff?style=for-the-badge&labelColor=0b0f14" alt="Free forever">
<img src="https://img.shields.io/badge/license-MIT-ffffff?style=for-the-badge&labelColor=0b0f14" alt="MIT">

</div>

<br/>

> **A note from the Phantera team.**
>
> We build Phantera with Claude Code every day. The waste we kept seeing was always the same: the most expensive model, at the highest effort, for jobs a cheap one did just as well.
>
> So we wrote the rule down, measured it, and turned it into a Claude Code plugin.
>
> It's yours. No sign-up, no trial, no upsell.
> **If it saves you a single dollar, pay us in stars.** ⭐

<br/>

## Install in one line

```text
/plugin install rightsize --marketplace phantera-ai/rightsize
```

From then on, every Claude Code session picks the right playbook, the right model (Haiku 5.5, Sonnet 5.5, Opus 5.5, Fable 5.1), the right effort (`low` to `max`), the right mode, and verification proportionate to the change. It escalates on evidence, never on habit.

<br/>

## Rule 0: quality before optimisation

The deliverable must reach the standard of the best expert in the field. Savings never come from weaker reasoning on it. They come from everything around it: lookups on cheap models, tests scoped to the change, no useless parallelism, a stable prompt cache.

When two tiers both look possible for the deliverable, rightsize takes the stronger one.

<br/>

## Measured, not claimed

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="docs/assets/routing-savings-dark.svg">
  <img src="docs/assets/routing-savings-light.svg" alt="Routed runs against Opus at high: minus 98, 96 and 73 percent, with 2 of 2 passes on both sides" width="100%">
</picture>

**Routing benchmark, 19 runs, against Opus at `high` for everything:**

| Task | Baseline | rightsize | Cost | Pass |
|---|---|---|---|---|
| Find a value in a repo, with decoys | $0.118 | haiku/low $0.002 | **−98%** | 2/2 vs 2/2 |
| Rename across files, add type hints | $0.104 | haiku/low $0.004 | **−96%** | 2/2 vs 2/2 |
| Fix a parser against hidden tests | $0.130 | sonnet/medium $0.035 | **−73%** | 2/2 vs 2/2 |

**Effort sweep, 100 valid headless runs.** Every valid run passed from `low` up, on Haiku, Sonnet and Opus 5.5. Haiku at `low` built a regex engine matching Python's `re` on all 3 000 random cases, 3 times out of 3, for **$0.02**.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="docs/assets/effort-cost-dark.svg">
  <img src="docs/assets/effort-cost-light.svg" alt="Mean cost relative to high effort, from low to max; every run passed" width="100%">
</picture>

| Cost vs `high`, same model | low | medium | xhigh | max |
|---|---|---|---|---|
| Sonnet 5.5 | 0.4–0.6× | 0.5–0.8× | 1.4–1.9× | 5.0–8.1× |
| Opus 5.5 | 0.6–1.1× | 0.9–1.0× | 1.5–2.2× | 3.7–9.3× (4–7× slower) |

**Scoped testing:** 11.4 s for the full suite, 0.7 s scoped after a one-module change.

What the numbers do not say: these tasks are well specified and verifiable, where low effort is safest. Nothing here measures open-ended work, and samples are small. Everything is reproducible with [`bench/`](docs/measuring.md).

<br/>

## How it works

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="docs/assets/how-it-works-dark.svg">
  <img src="docs/assets/how-it-works-light.svg" alt="Score the task, route it to a model, effort and mode, verify with the tests the change reaches, and escalate one rung on evidence" width="100%">
</picture>

| | |
|---|---|
| [`skills/rightsize/SKILL.md`](skills/rightsize/SKILL.md) | The strategy: rule 0, task scoring, routing table, modes, agent protocol, scoped verification, escalation, cache rules |
| [`skills/rightsize/PLAYBOOKS.md`](skills/rightsize/PLAYBOOKS.md) | Expert sequences: bug, feature, refactor, research, review, migration, performance, docs, sprint close |
| [`test_scope.py`](docs/scoped-testing.md) | Runs only the tests a change reaches, the full suite when that is the only safe answer |
| [`token_audit.py`](docs/measuring.md) | Where your tokens and dollars go, from local transcripts |
| [`agent_audit.py`](docs/agents-and-protocol.md) | Finds agents without `model` / `effort` and proposes values |
| [`agents/`](docs/agents-and-protocol.md) | `rs-scout` (haiku/low), `rs-verifier` (haiku/low), `rs-builder` (sonnet/medium), `rs-sage` (opus/high) |
| [`hooks/`](docs/architecture.md) | Rules in every session (~200 tokens, once) and in every sub-agent brief (~130 tokens) |

Guides: [Getting started](docs/getting-started.md) · [Usage](docs/usage-guide.md) · [Effort and models](docs/effort-and-models.md) · [Scoped testing](docs/scoped-testing.md) · [Measuring](docs/measuring.md) · [Architecture](docs/architecture.md) · [FAQ](docs/faq.md)

Requirements: Claude Code 2.1.275 or later, Python 3.9+, git. No runtime dependencies.

<br/>

## This is the first gift, not the last

Every tool we build to run Phantera better and that can help you too, we'll give back here.

**Star this repo and watch [phantera-ai](https://github.com/phantera-ai)** to get the next one the day it ships.

<br/>

<div align="center">

<a href="https://github.com/phantera-ai/rightsize/stargazers"><img src="https://img.shields.io/badge/%E2%AD%90%20Pay%20us%20in%20stars-it's%20the%20only%20price-00d4ff?style=for-the-badge&labelColor=0b0f14" alt="Pay us in stars"></a>

<br/><br/>

<sub>Made by the team behind <a href="https://www.phantera-tn.com/en"><b>Phantera</b></a>, B2B prospecting that knows when to stay quiet.<br/>Written by Ayoub Hammoudi · MIT · Contributions welcome, see <a href="CONTRIBUTING.md">CONTRIBUTING.md</a></sub>

</div>
