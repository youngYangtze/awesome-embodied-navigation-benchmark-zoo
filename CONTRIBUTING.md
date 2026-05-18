# Contributing

[English](CONTRIBUTING.md) | [简体中文](CONTRIBUTING.zh-CN.md)

Contributions should make the benchmark zoo easier to compare, reproduce, or navigate.

## Add a Benchmark

Please update `data/benchmarks.yml` and include:

- stable `id`
- benchmark name and year
- task family
- environment type
- simulator
- dataset and access status
- goal type
- observation modalities
- action space
- metrics
- dataset size (e.g. number of episodes, scenes, instructions)
- license (license of code and data, with caveats for upstream assets)
- official project, code, paper, and leaderboard links where available
- reproducibility status

## Reproducibility Status

Use the labels defined in `docs/reproducibility.md`:

- `verified`
- `partial`
- `archival`
- `needs-review`

## Curation Rules

- Prefer official project pages, official GitHub repositories, papers, and benchmark pages.
- Do not add a benchmark only because it is popular; it must have a navigation-centered evaluation task.
- Do not copy tables wholesale from papers or websites.
- Keep notes factual and short.
- Mention access restrictions for datasets, simulators, and leaderboards.

## Pull Request Checklist

- The entry has a unique `id`.
- The benchmark is navigation-centric.
- Required links are official when possible.
- Metrics and action space are filled in.
- Reproducibility status is conservative.
- The README table is updated if the benchmark is important enough for the seed list.
