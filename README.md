# how-to-metrics

**Metrics 正确打开方式** — An agent skill for building useful metrics without making the system worse.

让 agent 基于明确的统计口径、性能预算和故障隔离原则，分析、审查、新增和修改 Metrics。支持 Prometheus、OpenTelemetry 及其他监控平台；按实际 SDK 和后端语义工作。

## 它能做什么

- **Analyze**：追踪指标从业务事件到看板查询的完整路径，解释数据来源、计数边界及成本。
- **Review**：审查埋点、采集器、查询和告警，用代码位置、触发条件与影响支撑发现。
- **Write / Modify**：实现或修复指标，检查异常路径、标签范围、消费者兼容性和验证结果。

核心原则：

1. 先明确指标要回答的问题，再选择类型、单位和标签。
2. 业务路径复用已有结果，在内存中聚合；不为打点额外同步读写数据库或调用远程服务。
3. 昂贵采集必须有周期、超时、并发、归属和新鲜度设计。
4. 标签组合和资源使用有界；异步不等于零成本。
5. 遥测故障不破坏业务；零值、缺失值、旧值必须区分。
6. 指标与查询口径一致，修改前检查告警和看板依赖。

## 安装

将仓库放到 agent 的技能目录中。以 Codex 的默认个人技能目录为例：

```bash
git clone https://github.com/TripleCloud/how-to-metrics.git ~/.codex/skills/how-to-metrics
```

如果目标目录已存在，请更新已有安装，不要覆盖本地修改。其他支持 `SKILL.md` 的 agent 可按其技能目录约定安装。

也可以让 agent 读取本仓库的 [SKILL.md](SKILL.md)，按其中的工作流执行。

## 使用示例

```text
使用 $how-to-metrics review 这个 MR 中的埋点，重点检查数据库压力和高基数标签。
```

```text
使用 $how-to-metrics 给创建任务接口增加请求数、耗时和在途指标，并验证异常、取消及重试口径。
```

```text
使用 $how-to-metrics 分析这个 exporter 为什么增加了数据库负载，给出证据和最小修复方案。
```

```text
使用 $how-to-metrics 检查错误率与 P99 查询，特别关注多实例聚合、零流量和缺失数据。
```

## 预期交付

Review 会报告 **位置 → 触发条件 → 实际影响 → 最小修复建议**，并区分已证实缺陷与待确认信息。

实现任务会交付代码及最终统计口径、成本/兼容性影响、实际验证结果与剩余限制。只做静态检查时，不会宣称性能或线上行为已经验证。

## 内容结构

| 文件 | 用途 |
| --- | --- |
| [SKILL.md](SKILL.md) | 任务范围、执行工作流与共同约束 |
| [采集与成本](references/collection-and-cost.md) | 热路径、主动查询、快照和过载 |
| [语义与验证](references/semantics-and-validation.md) | 类型、标签、查询、迁移和风险相称的验证 |
| [官方来源](references/sources.md) | Prometheus 与 OpenTelemetry 官方依据 |
| [agents/openai.yaml](agents/openai.yaml) | 展示名称与默认调用提示词 |

## 适用边界

面向运行监控 Metrics，不替代产品行为事件分析、财务账本或精确审计系统，也不负责纯看板样式设计。

这些是基于行业原则整理的工程约束，不是统一认证标准。不会强制所有指标异步、所有 exporter 缓存，或使用一刀切的性能阈值。实际 SDK、业务契约和资源预算决定具体实现。

Skill 不授予生产数据库查询、压测、部署或消息发送权限；执行范围以用户请求与项目规则为准。
