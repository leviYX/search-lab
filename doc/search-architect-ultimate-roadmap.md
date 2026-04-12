# 搜索架构师最高阶学习路线图

更新时间：2026-04-11

这份路线图面向你的最高目标：不是“搜索优化工程师”，也不是“搜索负责人”，而是 `搜索架构师`。

这里的“搜索架构师”指的是：你不仅能调优某个模块，还能主导 `数据 -> 索引 -> Query 理解 -> 多路召回 -> 粗排 -> 精排 -> 业务重排 -> 展示 -> 日志回流 -> 训练闭环 -> 实验平台 -> 架构治理` 的完整系统，并在效果、延迟、稳定性、成本、迭代效率之间做系统级权衡。

如果你真以这个目标要求自己，那你的学习重点就不能只是：

- IR 基础
- Elasticsearch 使用
- 一点排序模型
- 一点向量检索

而必须升级为：

- 能设计搜索系统，不只是使用搜索系统
- 能定义数据标准，不只是消费数据
- 能主导训练闭环，不只是调用模型
- 能搭建实验机制，不只是看单次结果
- 能做容量、延迟、成本、SLA 治理，不只是盯相关性
- 能抽象方法论，带团队持续演进

## 1. 最高目标的能力标准

你最终要达到的不是“会做几个专项”，而是下面 8 个标准同时成立：

1. 能独立设计并评审一套千万到亿级 POI 搜索架构。
2. 能把 POI 数据构建、融合、去重、质量治理纳入搜索主链路。
3. 能为 `brand/address/category/nearby/route/ambiguous` 六大类 query 设计不同链路。
4. 能搭建多路召回、粗排、精排、业务重排的分层架构。
5. 能让模型真正进入生产：训练样本、特征、偏差、部署、监控、回滚都清楚。
6. 能建立完整评估体系：离线标注、在线 A/B、护栏指标、实验归因。
7. 能治理索引更新、时效性、延迟、缓存、容量、成本。
8. 能输出架构原则、规范、模板、技术方案，并带动团队长期演进。

## 2. 搜索架构师的 12 大能力模块

1. 信息检索与相关性理论
2. Lucene / ES / OpenSearch 内核与索引机制
3. POI 数据建模、融合、清洗、实体治理
4. Query 理解、纠错、Suggest、Rewrite、意图识别
5. 本地搜索领域能力：地址、nearby、along-route、geo constraint
6. 多路召回与召回路由
7. 粗排架构
8. 精排架构与 LTR
9. 业务重排、去重、多样性、展示层策略
10. 日志回流、训练闭环、偏差校正、实验平台
11. 分布式搜索架构、索引构建、性能治理、稳定性治理
12. 负责人/架构师能力：方法论、方案评审、灰度回滚、跨团队协同

注意：`3/4/5/6/7/8/9/10/11/12` 才是架构师和普通搜索工程师的分水岭。

## 3. 架构师必须掌握的全链路

你必须把所有线上问题都映射到这条链路：

`数据接入 -> 清洗 -> 融合 -> 去重 -> 质量分 -> 实体建模 -> 索引构建 -> 增量更新 -> Query 规范化 -> 纠错 -> Query 分类 -> 意图识别 -> Suggest -> 多路召回 -> 粗排 -> 精排 -> 业务重排 -> 展示 -> 埋点 -> 样本构建 -> 训练 -> 模型发布 -> A/B -> 监控 -> 灰度 -> 回滚`

这条链路里任何一个点出问题，最终都会表现成“搜索效果差”。架构师的核心能力，就是把症状拆回链路。

## 4. 哪些环节必须学模型，哪些环节不能只靠模型

## 4.1 必须模型化的核心环节

- Query 分类 / 意图识别
- Suggest 排序
- 长尾别名挖掘 / 同义词发现
- 精排
- 训练闭环与偏差治理
- 语义补召回
- POI 质量分预测
- 去重 / 实体匹配中的复杂判定

## 4.2 可以先规则、后模型的环节

- 拼写纠错
- 地址解析
- 召回路由
- 粗排
- nearby 基础排序
- 品牌主实体识别

## 4.3 不能交给纯模型的环节

- 业务重排
- 营业状态、风险规则、商业规则
- 灰度与回滚
- 索引时效性与构建链路
- SLA、容量、成本治理
- 去重后的展示与聚合策略

你要建立一个非常重要的工程观：`模型是搜索系统的一部分，不是搜索系统本身。`

## 5. 18 个月架构师路线

## 阶段 A：基础打牢，但按架构师方式打牢（第 0-3 月）

### A1. 第 0 月：评估体系与 badcase 基线

目标：

- 不凭感觉做优化，先建立证据系统。

重点：

- query taxonomy
- judgment set
- Recall / MRR / NDCG
- query 分桶
- 会话成功率
- 零结果率
- 首条满意率

交付物：

- `500+` query 离线评估集
- badcase 管理表
- query taxonomy：`brand/address/category/nearby/route/ambiguous/landmark`
- 一份当前系统问题地图

模型要求：

- 不上模型

### A2. 第 1 月：IR 与 Lucene 内核

目标：

- 不只会调用 ES API，要知道分数和延迟从哪里来。

重点：

- 倒排索引
- posting list
- BM25 / BM25F
- analyzer
- segment / merge / refresh
- explain / profile
- geo query

交付物：

- 极简倒排 demo
- BM25 baseline
- explain 报告

模型要求：

- 不上模型

### A3. 第 2 月：POI 数据建模与实体规范

目标：

- 定义“搜什么”的规范。

重点：

- canonical schema
- 主键设计
- 来源建模
- 地址字段体系
- 类目体系
- 品牌体系
- 营业状态和 freshness 字段

交付物：

- POI schema
- 字段字典
- 数据分层图

模型要求：

- 不上模型

### A4. 第 3 月：数据融合、去重、质量治理

目标：

- 打好底层可信度。

重点：

- 多源融合
- 冲突解决
- 同名不同实体
- 同实体多源归并
- 地址归一化
- 类目归一化
- 质量分

交付物：

- merge policy
- duplicate policy
- quality score baseline

模型要求：

- 规则 baseline 必做
- 开始尝试去重模型和质量分类模型

## 阶段 B：Query 侧与本地搜索侧做深（第 4-7 月）

### B1. 第 4 月：Query 理解总线

目标：

- 建一条统一 query pipeline。

重点：

- normalize
- spelling correction
- token rewrite
- query classification
- intent detection
- slot filling
- entity tagging

交付物：

- query parser
- query taxonomy v2
- query debug 工具

模型要求：

- Query 分类、意图识别建议上模型
- 规则和词典必须保留

### B2. 第 5 月：Suggest、别名、同义词、品牌词

目标：

- 把 query 输入侧做到“用户没输完你就知道要什么”。

重点：

- prefix recall
- autocomplete
- suggest ranking
- alias mining
- synonym discovery
- brand query understanding

交付物：

- suggest pipeline
- alias dictionary
- synonym governance 规范
- 品牌词展示策略

模型要求：

- Suggest 排序建议上模型
- 长尾别名挖掘建议上模型

### B3. 第 6 月：地址搜索与 geocoding

目标：

- 把地图搜索最深的模块之一吃透。

重点：

- free-form / structured address
- address parser
- address normalizer
- candidate generation
- confidence scoring
- reverse geocoding

交付物：

- address parser baseline
- geocoder baseline
- 地址 badcase 库

模型要求：

- parser 可先规则
- confidence score 建议上模型

### B4. 第 7 月：nearby、viewport、along-route

目标：

- 建立真正的本地搜索空间体系。

重点：

- location bias
- location restriction
- viewport search
- nearby retrieval
- route corridor
- detour cost
- travel mode

交付物：

- nearby baseline
- along-route baseline
- `address / nearby / route` 策略差异图

模型要求：

- nearby 可先规则
- route 排序中后期建议加模型

## 阶段 C：召回与排序体系工业化（第 8-12 月）

### C1. 第 8 月：多路召回

目标：

- 从单路检索升级到召回架构。

重点：

- lexical recall
- alias recall
- category recall
- brand recall
- geo recall
- structured address recall
- vector recall
- recall merge

交付物：

- 至少 6 路召回
- 召回覆盖率分析
- 召回融合策略

模型要求：

- semantic recall 建议模型化
- 其他召回先规则再模型

### C2. 第 9 月：召回路由与场景路由

目标：

- 不同 query 走不同链路。

重点：

- query routing
- scene routing
- fallback strategy
- route by intent
- route by geo context

交付物：

- query router baseline
- 路由收益分析

模型要求：

- 先规则路由
- 后期上 routing model

### C3. 第 10 月：粗排

目标：

- 在延迟约束内保住核心候选。

重点：

- filtering
- scoring
- lightweight features
- channel normalization
- latency budget

交付物：

- 粗排 baseline
- 误杀分析
- 延迟预算文档

模型要求：

- 先规则 / 线性模型
- 后期可上 LR / GBDT / 小 DNN

### C4. 第 11 月：精排

目标：

- 处理复杂相关性与特征交互。

重点：

- LTR
- feature engineering
- pointwise / pairwise / listwise
- label design
- click bias
- query bucket learning

交付物：

- `30-100` 个特征
- GBDT / LambdaMART baseline
- 分桶收益分析

模型要求：

- 必须上模型
- 这是主战场

### C5. 第 12 月：业务重排与展示层治理

目标：

- 把排序结果变成可用结果。

重点：

- business rerank
- dedup
- clustering
- diversity
- store-open prioritization
- sponsored coexistence
- risk control

交付物：

- business rulebook
- dedup / cluster 设计
- 展示层策略

模型要求：

- 规则主导
- 模型辅助

## 阶段 D：真正进入架构师区间（第 13-18 月）

### D1. 第 13 月：日志回流与训练样本系统

目标：

- 让系统具备持续学习能力。

重点：

- exposure / click / nav / conversion logs
- sample builder
- negative sampling
- train / val / test split
- feature snapshot

交付物：

- 样本构建规范
- 特征快照方案
- 训练数据版本管理方案

### D2. 第 14 月：偏差校正与实验归因

目标：

- 防止模型“越学越歪”。

重点：

- selection bias
- position bias
- counterfactual evaluation
- interleaving / A/B
- metric attribution

交付物：

- 偏差分析报告
- 实验归因模板
- 护栏指标体系

### D3. 第 15 月：索引构建架构与 freshness 治理

目标：

- 让搜索系统真正可生产。

重点：

- full build / incremental build
- CDC
- index versioning
- dual write / blue-green
- freshness SLA
- rollback

交付物：

- 索引构建架构图
- freshness 方案
- 回滚预案

### D4. 第 16 月：分布式服务与性能治理

目标：

- 让系统扛住流量、延迟和故障。

重点：

- sharding / replication
- cache
- request fanout
- timeout
- degradation
- circuit breaker
- p99 / p999

交付物：

- 服务拓扑图
- 性能压测报告
- 降级与熔断策略

### D5. 第 17 月：成本治理与资源效率

目标：

- 让系统不只是好用，还可长期经营。

重点：

- CPU / memory / storage cost
- index size
- ANN 成本
- cache hit ratio
- feature compute cost
- model serving cost

交付物：

- 成本看板
- 单 query 成本拆解
- 资源优化方案

### D6. 第 18 月：架构原则、方法论、团队治理

目标：

- 从做系统升级到带系统、带团队、带方向。

重点：

- 架构原则
- review checklist
- design template
- milestone management
- cross-team dependency management
- rollback culture

交付物：

- 搜索架构原则文档
- 搜索专项模板
- 一套团队级 review checklist

## 6. 你必须做的 10 个系统

如果你真要成为搜索架构师，下面 10 个系统或子系统至少要亲手做过简化版：

1. 最小 POI 检索系统
2. POI 数据融合与去重系统
3. Query parser / suggest 系统
4. 地址搜索 / geocoder 系统
5. nearby / along-route 检索系统
6. 多路召回系统
7. 粗排 + 精排系统
8. 业务重排与去重展示系统
9. 离线评估与 badcase 平台
10. 日志回流与训练样本系统

## 7. 你必须读的资料类型

不是只读论文，要读 5 类资料：

1. IR 教材：Stanford IR Book
2. 搜索引擎文档：Lucene / Elasticsearch / OpenSearch
3. 地图与本地搜索文档：Google Maps Platform / Nominatim / Pelias / libpostal / H3 / S2
4. Google Research / SIGIR / WWW / KDD 论文：LTR、bias correction、query understanding、semantic retrieval
5. 大型分布式系统资料：索引构建、流批架构、缓存、容灾、实验平台

## 8. 架构师级验收标准

当下面这些问题你都能回答得很硬，你才接近搜索架构师：

- 为什么这个 badcase 根因在数据层，不在排序层？
- 为什么这个 query 应该走 `address recall + geo filter + address rerank`，而不是普通 POI 搜索？
- 为什么这里粗排不用复杂模型，精排必须上模型？
- 为什么业务重排不能交给一个黑盒模型？
- 为什么向量召回在某些长尾 query 有价值，但品牌词和地址词风险更高？
- 为什么你的索引更新架构能保证 freshness，但不会把线上稳定性打爆？
- 为什么你的训练数据不会因为 exposure bias 导致模型失真？
- 为什么你的实验结果可信，且知道收益来自哪一层？
- 为什么你的系统在 p99、成本、索引大小、效果之间做了正确权衡？

## 9. 最后一句话

搜索架构师的门槛，不是你会不会调 BM25，也不是你会不会训一个排序模型。

真正的门槛是：

- 你能不能把复杂问题拆成链路问题
- 你能不能让数据、规则、模型、系统协同工作
- 你能不能把效果、延迟、稳定性、成本放在同一个框架里治理
- 你能不能持续让团队和系统一起进化

如果你愿意按这条路线走两年，并且每个阶段都有系统、有实验、有复盘、有文档，你的上限会非常高。
