# 搜索架构师 24 个月执行计划

更新时间：2026-04-11

这份文档不是概念路线，而是执行版。目标是让你按 24 个月推进，逐步从搜索工程师走到搜索架构师。默认每周投入 `10-15h`，其中：

- `3h` 理论阅读
- `4h` 编码实验
- `3h` badcase 与日志分析
- `2h` 总结、复盘、文档输出

每个月按 4 周推进，每周都必须有产出。

## 第 1 阶段：打基础，但按架构师方式打基础（第 1-6 月）

## 第 1 月：评估与基线

目标：建立证据系统。

- 第 1 周：整理当前搜索链路，梳理 query 类型，建立 `brand/address/category/nearby/route/ambiguous` taxonomy。
- 第 2 周：抽取 `200-300` 条 query，定义 4 级相关性标注规范。
- 第 3 周：跑离线评估，产出 baseline 指标：`Recall@10 / MRR / NDCG@5 / NDCG@10`。
- 第 4 周：建立 badcase 池，按 `data/query/recall/rank/geo` 五大类归因。

月度产出：

- query taxonomy
- judgment set v1
- baseline 指标报告
- badcase 周报模板

## 第 2 月：IR 与 Lucene 基础

目标：理解检索和打分的底层原理。

- 第 1 周：手写极简倒排索引 demo，理解 token -> posting list。
- 第 2 周：实现 BM25 baseline，对比不同字段权重。
- 第 3 周：读 Lucene segment / merge / refresh，分析时效性与资源的关系。
- 第 4 周：做 explain 拆解，选 10 个 badcase 做逐项打分分析。

月度产出：

- 倒排 demo
- BM25 baseline
- explain 分析报告

## 第 3 月：POI 数据建模

目标：定义实体和字段标准。

- 第 1 周：设计 canonical POI schema，梳理主键、来源 ID、canonical ID。
- 第 2 周：梳理名称、别名、地址、品牌、类目、营业状态、时效字段。
- 第 3 周：定义行政区、道路、门牌、楼栋、商圈等层级字段。
- 第 4 周：输出字段字典、枚举规范、空值策略、默认值策略。

月度产出：

- POI schema
- 字段字典
- 数据分层图

## 第 4 月：数据融合、清洗、去重

目标：打好实体可信度底座。

- 第 1 周：梳理多源数据接入方式，定义 source priority。
- 第 2 周：设计 merge policy，处理字段冲突、时间冲突、状态冲突。
- 第 3 周：设计 duplicate policy，覆盖同名、别名、近距离、品牌门店。
- 第 4 周：建立质量分 baseline，评估名称完整度、地址完整度、坐标可信度。

月度产出：

- merge policy
- duplicate policy
- quality score v1

## 第 5 月：索引设计与基础 POI 搜索

目标：用干净数据搭建可解释 baseline。

- 第 1 周：建立索引，覆盖 `name/alias/address/category/brand/location/city/district/status`。
- 第 2 周：为 `name/alias/address/category` 设计不同 analyzer。
- 第 3 周：实现基础检索：名称搜、别名搜、地址搜、类目搜。
- 第 4 周：分析 20 个 badcase，形成字段与 analyzer 调优结论。

月度产出：

- baseline 索引
- analyzer 设计说明
- 检索 badcase 报告

## 第 6 月：Query 理解与 Suggest 基线

目标：建立 query 处理总线。

- 第 1 周：做 normalize，处理全半角、空格、大小写、数字、简称。
- 第 2 周：实现 query 分类 baseline，先规则后轻量模型。
- 第 3 周：搭 suggest pipeline，做 prefix recall、去重、截断。
- 第 4 周：实现 rewrite baseline，覆盖别名、品牌简称、行政区简称。

月度产出：

- query parser v1
- suggest pipeline v1
- rewrite 规则清单

## 第 2 阶段：进入本地搜索主战场（第 7-12 月）

## 第 7 月：别名、同义词、品牌词

目标：建立长期可维护的语义治理体系。

- 第 1 周：梳理 alias、synonym、brand 的边界。
- 第 2 周：建立人工词典与维护规范。
- 第 3 周：做长尾别名挖掘 baseline，尝试统计法或向量法。
- 第 4 周：定义品牌主实体与门店实体的召回与展示策略。

月度产出：

- alias/synonym/brand 规范
- 品牌词策略文档

## 第 8 月：地址搜索与 geocoder

目标：建立独立地址链路。

- 第 1 周：做 free-form address parser，拆行政区、道路、门牌、楼栋。
- 第 2 周：做地址归一化，统一简称、道路写法、门牌格式。
- 第 3 周：做 candidate generation，支持结构化召回与 free-form 兜底。
- 第 4 周：做 address confidence scoring，并整理失败模式。

月度产出：

- geocoder baseline
- 地址 badcase 清单
- address confidence 方案

## 第 9 月：nearby 与空间约束

目标：把 local relevance 拉进主链路。

- 第 1 周：实现 geo filter、geo sort、distance feature。
- 第 2 周：做 nearby baseline，比较文本优先与距离优先。
- 第 3 周：引入 viewport、行政区约束、商圈约束。
- 第 4 周：按 `nearby/category/landmark` 分桶分析收益与副作用。

月度产出：

- nearby baseline
- 空间特征实验报告

## 第 10 月：along-route 与出行场景

目标：把路线搜索从 nearby 中分离出来。

- 第 1 周：理解 route corridor、detour cost、travel mode。
- 第 2 周：建立 along-route candidate generation。
- 第 3 周：引入 detour、营业状态、类目偏好等排序特征。
- 第 4 周：做 `nearby vs along-route` 差异化策略总结。

月度产出：

- along-route baseline
- 路线搜索策略图

## 第 11 月：多路召回

目标：从单路检索升级到召回架构。

- 第 1 周：实现 lexical recall、alias recall。
- 第 2 周：实现 category recall、brand recall。
- 第 3 周：实现 geo recall、address structured recall。
- 第 4 周：做 recall merge 与 coverage 分析。

月度产出：

- 至少 6 路召回
- recall coverage 报告

## 第 12 月：召回路由

目标：不同 query 走不同召回链路。

- 第 1 周：定义 route by query type。
- 第 2 周：定义 route by geo context。
- 第 3 周：设计 fallback 与兜底策略。
- 第 4 周：比较规则路由和轻量 routing model。

月度产出：

- recall router v1
- 路由收益报告

## 第 3 阶段：排序体系工业化（第 13-18 月）

## 第 13 月：粗排

目标：高召回、低误杀、低延迟。

- 第 1 周：定义粗排输入、输出、延迟预算。
- 第 2 周：设计轻量特征：文本、类目、距离、行政区、质量分、营业状态。
- 第 3 周：做规则或线性模型 baseline。
- 第 4 周：做误杀分析与延迟分析。

月度产出：

- 粗排 baseline
- 粗排误杀分析
- 延迟预算文档

## 第 14 月：精排特征工程

目标：为精排准备高质量特征体系。

- 第 1 周：整理 query-POI 文本匹配特征。
- 第 2 周：整理 geo、quality、behavior、freshness 特征。
- 第 3 周：做特征口径统一与快照设计。
- 第 4 周：分析哪些特征适合粗排，哪些只适合精排。

月度产出：

- `30-80` 个特征清单
- 特征治理文档

## 第 15 月：精排模型 baseline

目标：建立精排主战场。

- 第 1 周：构建训练样本，定义正负样本规则。
- 第 2 周：训练 GBDT / LambdaMART baseline。
- 第 3 周：做 query 分桶收益分析：品牌词、地址词、类目词、nearby、route。
- 第 4 周：做 explainability 与特征重要性分析。

月度产出：

- 精排模型 baseline
- 分桶收益报告

## 第 16 月：业务重排

目标：把“相关”变成“可用”。

- 第 1 周：设计营业状态、时间敏感性、风险规则。
- 第 2 周：设计主品牌/分店、去重、聚合、多样性策略。
- 第 3 周：处理商业规则与自然结果共存。
- 第 4 周：做 business rerank 前后对比评估。

月度产出：

- business rerank rulebook
- dedup/cluster 策略说明

## 第 17 月：语义补召回与 TopK rerank

目标：引入现代语义能力，但不破坏主链路稳定性。

- 第 1 周：做向量召回 baseline，验证长尾 query 收益。
- 第 2 周：做 hybrid merge，对比 lexical/vector/hybrid。
- 第 3 周：做 TopK rerank baseline。
- 第 4 周：明确哪些 query 不适合语义主导。

月度产出：

- hybrid 检索实验报告
- 语义适用边界说明

## 第 18 月：排序体系复盘

目标：完成召回-粗排-精排-重排的整体打通。

- 第 1 周：绘制完整排序链路图。
- 第 2 周：做跨层归因，判断收益来自哪一层。
- 第 3 周：梳理副作用：延迟、误杀、偏差、业务冲突。
- 第 4 周：输出排序体系方法论总结。

月度产出：

- 全链路排序架构图
- 排序体系总结

## 第 4 阶段：训练闭环与生产架构（第 19-24 月）

## 第 19 月：日志回流与样本系统

目标：建立持续学习能力。

- 第 1 周：设计 exposure/click/navigation/conversion 埋点。
- 第 2 周：定义 sample builder。
- 第 3 周：设计 feature snapshot 与数据版本。
- 第 4 周：建立训练数据回溯链路。

月度产出：

- 日志字典
- 样本构建规范
- feature snapshot 方案

## 第 20 月：偏差校正与实验体系

目标：让模型训练和效果归因可信。

- 第 1 周：学习 selection bias、position bias。
- 第 2 周：建立 counterfactual / debias 思路。
- 第 3 周：设计线上 A/B 实验流程与护栏指标。
- 第 4 周：设计实验归因模板。

月度产出：

- 偏差分析报告
- 实验归因模板
- 护栏指标定义

## 第 21 月：索引构建与 freshness

目标：让索引系统进入可生产状态。

- 第 1 周：设计 full build / incremental build。
- 第 2 周：引入 CDC、版本切换、蓝绿发布。
- 第 3 周：设计 freshness SLA、延迟监控、异常修复流程。
- 第 4 周：编写回滚与灾备方案。

月度产出：

- 索引构建架构图
- freshness 治理方案
- 回滚预案

## 第 22 月：分布式服务与性能治理

目标：扛流量、控延迟、稳服务。

- 第 1 周：设计 query service、rank service、feature service 拆分。
- 第 2 周：设计 sharding、replication、fanout、cache。
- 第 3 周：压测并分析 p95/p99/p999。
- 第 4 周：设计降级、限流、熔断与兜底。

月度产出：

- 服务拓扑图
- 性能压测报告
- 降级策略

## 第 23 月：成本治理

目标：做可长期经营的搜索系统。

- 第 1 周：拆解索引存储成本、缓存成本、模型服务成本。
- 第 2 周：建立单 query 成本模型。
- 第 3 周：分析 ANN、复杂特征、rerank 带来的资源代价。
- 第 4 周：产出资源优化方案。

月度产出：

- 成本看板
- 单 query 成本拆解
- 资源优化报告

## 第 24 月：架构师方法论与团队治理

目标：完成从工程师到架构师的跃迁。

- 第 1 周：沉淀搜索架构原则：分层、可解释、可评估、可回滚。
- 第 2 周：沉淀 review checklist、方案模板、专项模板。
- 第 3 周：做一次完整架构评审和内部分享。
- 第 4 周：输出 2 年总结，明确下一阶段方向。

月度产出：

- 搜索架构原则文档
- review checklist
- 内部分享材料
- 两年总结

## 每季度必须完成的检查点

- 至少新增一类可复用系统能力
- 至少完成一次跨层归因分析
- 至少完成一次专项复盘
- 至少输出一份结构化方案
- 至少修掉一类反复出现的 badcase

## 执行纪律

这份计划只有在你满足下面 5 条时才有效：

1. 每周都写总结，不允许只学不沉淀。
2. 每月都做实验，不允许只看论文。
3. 每季度都做系统级复盘，不允许只看局部指标。
4. 每次收益都要归因，不允许“感觉变好了”。
5. 每次方案都要写回滚，不允许只写优化不写风险。
