# Reproducibility Policy

[English](reproducibility.md) | [简体中文](reproducibility.zh-CN.md)

The zoo tracks practical reproducibility, not just whether a paper says code is public.

## Status Labels

### verified

Use this when all of the following are available:

- public code or starter kit
- public dataset or clear access procedure
- documented evaluation command or submission process
- metrics are defined clearly
- at least one baseline or example submission exists

### partial

Use this when reproduction is possible but has meaningful friction:

- external terms or private simulator assets are required
- instructions are incomplete
- leaderboard is closed but local evaluation exists
- baseline code exists but is stale
- results depend on manual setup that is not fully scripted

### archival

Use this when the benchmark is historically important but not a strong target for new submissions:

- repository is read-only or unmaintained
- leaderboard is inactive
- dependencies are old or difficult to build
- public evaluation is no longer clearly supported

### needs-review

Use this for candidate entries that need verification before being treated as reliable.

## Review Checklist

For every new benchmark entry, check:

- Does the project define a navigation task clearly?
- Is the dataset available or is the access process documented?
- Is the simulator or environment specified?
- Are observations and action spaces specified?
- Are metrics specified?
- Is there a public evaluator, leaderboard, or local evaluation script?
- Are baseline results and code available?
- Are license and usage restrictions noted?

## Avoid Overclaiming

Do not mark an entry as `verified` just because code exists. If data access is restricted, scripts are missing, or evaluation is unclear, use `partial`.
