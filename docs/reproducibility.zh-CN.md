# 可复现政策

[English](reproducibility.md) | [简体中文](reproducibility.zh-CN.md)

本 zoo 追踪实践意义上的可复现性，而不只是论文是否声称代码公开。

## 状态标签

### verified

当以下内容全部可用时使用：

- 公开代码或 starter kit
- 公开 dataset 或清晰的访问流程
- 有文档说明的评测命令或提交流程
- metrics 定义清楚
- 至少有一个 baseline 或 example submission

### partial

当复现可行但存在明显摩擦时使用：

- 需要外部条款授权或私有 simulator assets
- instructions 不完整
- leaderboard 已关闭，但本地 evaluation 可用
- baseline code 存在但已经陈旧
- 结果依赖未完全脚本化的手动设置

### archival

当 benchmark 有历史价值，但不太适合作为新 submission 目标时使用：

- repository 只读或不再维护
- leaderboard 不活跃
- dependencies 陈旧或难以构建
- public evaluation 不再被清晰支持

### needs-review

用于候选条目。在被视为可靠条目前，需要进一步验证。

## Review Checklist

每个新增 benchmark 条目都应检查：

- 项目是否清晰定义了导航任务？
- dataset 是否可用，或访问流程是否有文档？
- simulator 或 environment 是否明确？
- observations 与 action spaces 是否明确？
- metrics 是否明确？
- 是否有 public evaluator、leaderboard 或 local evaluation script？
- baseline results 和 code 是否可用？
- license 与 usage restrictions 是否已标注？

## 避免过度声明

不要仅因为存在代码就把条目标为 `verified`。如果 data access 受限、scripts 缺失或 evaluation 不清楚，应使用 `partial`。
