# 依据与适用边界

本 skill 把行业原则转成工程决策约束，数据库预算、审查方式和案例是落地建议，不是逐字引用的官方 MUST。没有“开销必须小于 1%”“每项指标只能 10 个标签组合”等跨项目固定门槛。优先尊重当前项目契约和明确业务要求，并展示取舍。

按问题查对应官方资料；版本敏感能力以实际 SDK/后端版本核对：

- [Prometheus instrumentation](https://prometheus.io/docs/practices/instrumentation/)：埋点、热路径、类型与初始化。
- [Writing exporters](https://prometheus.io/docs/instrumenting/writing_exporters/)：昂贵采集、抓取、缓存例外及失败表达。
- [Metric and label naming](https://prometheus.io/docs/practices/naming/)：Prometheus 命名、单位和标签原则。
- [Histograms and summaries](https://prometheus.io/docs/practices/histograms/)：桶、分位数、聚合和 Native Histogram。
- [Query functions](https://prometheus.io/docs/prometheus/latest/querying/functions/)：查询函数实际语义。
- [OTel performance](https://opentelemetry.io/docs/specs/otel/performance/)：非阻塞、有界资源与过载取舍。
- [OTel error handling](https://opentelemetry.io/docs/specs/otel/error-handling/)：运行时遥测异常隔离。
- [OTel Metrics SDK](https://opentelemetry.io/docs/specs/otel/metrics/sdk/)：聚合、采集、View、基数限制等。

本 skill 自包含，不依赖内部文档、账号或特定监控平台的访问权限。
