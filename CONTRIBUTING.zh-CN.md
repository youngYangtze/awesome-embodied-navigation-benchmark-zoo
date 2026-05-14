# 贡献指南

[English](CONTRIBUTING.md) | [简体中文](CONTRIBUTING.zh-CN.md)

贡献内容应让这个 benchmark zoo 更容易比较、更容易复现、更容易导航。

## 添加 Benchmark

请更新 `data/benchmarks.yml`，并包含：

- 稳定的 `id`
- benchmark 名称和年份
- 任务族
- 环境类型
- simulator
- dataset 与访问状态
- 目标类型
- observation modalities
- action space
- metrics
- 官方项目、代码、论文和 leaderboard 链接，如果可用
- reproducibility status

## 可复现状态

使用 [docs/reproducibility.zh-CN.md](docs/reproducibility.zh-CN.md) 中定义的标签：

- `verified`
- `partial`
- `archival`
- `needs-review`

## 策展规则

- 优先使用官方项目页、官方 GitHub 仓库、论文和 benchmark 页面。
- 不要只因为某个 benchmark 热门就添加；它必须有以导航为中心的评测任务。
- 不要整段复制论文或网站中的表格。
- notes 保持事实性和简短。
- 标明 dataset、simulator 和 leaderboard 的访问限制。

## Pull Request Checklist

- 条目有唯一的 `id`。
- benchmark 以导航为中心。
- 必要链接尽量使用官方来源。
- metrics 和 action space 已填写。
- reproducibility status 使用保守判断。
- 如果该 benchmark 足够重要，README seed list 也已更新。
