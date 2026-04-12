# 搜索架构师必读资料、必做实验、必拆源码清单

更新时间：2026-04-11

这份文档回答 3 个问题：

- 该读什么
- 该做什么实验
- 该拆哪些源码

目标不是把资料堆满，而是让每份输入都服务于你的架构师目标。

## 1. 必读资料分层

## 1.1 第一层：IR 与检索引擎基础

必读：

- Stanford IR Book
- Lucene 官方文档
- Elasticsearch 官方文档
- OpenSearch 官方文档

重点章节：

- 倒排索引
- BM25 / BM25F
- 查询处理
- 相关性评估
- 多字段检索
- geo query
- explain / profile

输出要求：

- 一份《倒排、BM25、字段权重、explain 的一阶原理》总结

## 1.2 第二层：Google 公开资料

必读：

- Google Search Central: How Search Works
- Google Search Central: Ranking Systems Guide
- Google Maps Platform: Place Autocomplete
- Google Maps Platform: Text Search
- Google Maps Platform: Search Along Route
- Google Maps Platform: Geocoding / Address Validation

你要重点学的不是 API 本身，而是它们暗含的产品与系统拆分：

- Search 是 `indexing + serving + ranking systems`
- Maps Search 区分 `autocomplete / text search / nearby / along-route`
- 地址不是普通文本，而是结构化与校验问题
- 位置 bias、位置 restriction、路线 corridor 是本地搜索独有约束

输出要求：

- 一份《Google 公开资料里透露出的本地搜索架构原则》总结

## 1.3 第三层：本地搜索与地址系统

必读：

- Nominatim 文档
- Pelias 架构与导入链路
- libpostal
- H3 文档
- S2 Geometry

重点：

- 地址解析
- 地址归一化
- geocoder 设计
- 空间索引
- 数据导入和更新链路

输出要求：

- 一份《Nominatim / Pelias / libpostal / H3 / S2 对比表》

## 1.4 第四层：学习排序、偏差、现代检索

建议主题：

- Learning to Rank
- selection bias / position bias
- counterfactual evaluation
- query auto-completion
- semantic retrieval
- hybrid retrieval
- reranking

读法要求：

- 不要只读 abstract
- 每篇论文至少回答：
  - 它解决什么问题
  - 适用哪个链路
  - 在地图搜索里有哪些边界
  - 是否值得做实验

输出要求：

- 一份《论文阅读卡片库》

## 1.5 第五层：分布式系统与生产架构

必读主题：

- 索引构建
- CDC
- 数据版本化
- 蓝绿发布
- 分布式缓存
- fanout
- 熔断、限流、降级
- 监控、告警、SLA

输出要求：

- 一份《搜索生产架构 checklist》

## 2. 必做实验清单

## 2.1 检索与索引实验

必须做：

1. 极简倒排索引
2. BM25 baseline
3. 多字段权重对比实验
4. analyzer 对比实验
5. geo filter vs geo score 对比实验

验收：

- 你能解释为什么 badcase 分数异常

## 2.2 数据治理实验

必须做：

1. POI schema 设计
2. merge policy 实验
3. duplicate policy 实验
4. quality score baseline
5. 地址归一化实验

验收：

- 你能拿出一批具体样本说明哪些合并正确，哪些错合并

## 2.3 Query 理解实验

必须做：

1. query taxonomy 标注
2. 纠错 baseline
3. query 分类 baseline
4. slot filling baseline
5. suggest pipeline
6. rewrite baseline

验收：

- 你能解释一个 query 为什么要走某条链路

## 2.4 本地搜索实验

必须做：

1. address parser baseline
2. geocoder baseline
3. nearby baseline
4. along-route baseline
5. route detour 排序实验

验收：

- 你能说明 `address / nearby / route` 三类策略为什么不能共用

## 2.5 召回实验

必须做：

1. lexical recall
2. alias recall
3. category recall
4. brand recall
5. geo recall
6. structured address recall
7. vector recall
8. hybrid merge
9. recall router

验收：

- 你能画出召回覆盖率图并知道各通道的价值与副作用

## 2.6 排序实验

必须做：

1. 粗排规则 baseline
2. 粗排轻量模型 baseline
3. 精排特征工程
4. GBDT / LambdaMART baseline
5. business rerank
6. TopK rerank
7. 分桶收益分析

验收：

- 你能证明收益来自粗排、精排还是重排

## 2.7 训练闭环实验

必须做：

1. exposure/click/nav/conversion 埋点设计
2. sample builder
3. negative sampling
4. position bias 分析
5. counterfactual 思路试验
6. A/B 方案与护栏指标设计

验收：

- 你能说明为什么这套训练数据可信

## 2.8 生产架构实验

必须做：

1. full build / incremental build 方案
2. 索引版本切换
3. freshness 监控
4. fanout 与 cache 实验
5. p95 / p99 压测
6. 降级方案演练

验收：

- 你能说清索引更新、稳定性、延迟和成本的权衡

## 3. 必拆源码清单

## 3.1 Lucene

重点拆：

- analyzer
- query rewrite
- similarity
- segment / merge
- explain

拆解问题：

- 打分从哪里来
- segment 为什么影响时效性和资源
- explain 为什么能解释 badcase

## 3.2 Elasticsearch / OpenSearch

重点拆：

- mapping
- analyzer
- geo query
- combined_fields
- rank eval
- profiling

拆解问题：

- 多字段如何协同
- geo 相关查询如何影响召回和排序
- 如何做评估和 profile

## 3.3 Nominatim

重点拆：

- 数据导入
- tokenizer
- 查询处理
- address search
- reverse geocode

拆解问题：

- 地址搜索为什么不是普通全文检索
- tokenizer 如何影响地址召回

## 3.4 Pelias

重点拆：

- importer
- API 分层
- geocoder 组织方式
- 数据流

拆解问题：

- 为什么 geocoder 要按组件拆服务
- 数据导入与服务层如何解耦

## 3.5 libpostal

重点拆：

- parser
- normalization
- language / locale 处理

拆解问题：

- 地址结构化为什么难
- 规则和模型边界在哪里

## 3.6 H3 / S2

重点拆：

- 空间切分
- 邻域关系
- 不同粒度的适用边界

拆解问题：

- nearby 和区域约束为什么需要空间索引

## 4. 论文阅读方法

不要按“知名论文列表”乱读，按链路读：

- Query 理解：纠错、分类、意图识别、自动补全
- 召回：semantic recall、hybrid retrieval、query routing
- 排序：LTR、bias correction、rerank
- 数据：entity matching、dedup、quality prediction
- 系统：freshness、index build、large-scale serving

每篇论文必须输出：

- 问题定义
- 方法核心
- 依赖数据
- 可上线性
- 适用场景
- 风险
- 下一步实验

## 5. 你的输出物清单

如果你真的按这份文档执行，24 个月后至少应该留下：

- 1 套 query taxonomy
- 1 套 judgment set
- 1 套 POI schema
- 1 套 merge / duplicate / quality policy
- 1 条 query parser / suggest pipeline
- 1 套 address / nearby / route baseline
- 1 套多路召回系统
- 1 套粗排 / 精排 / business rerank 系统
- 1 套样本构建与实验流程
- 1 套索引构建与生产架构设计

这才说明你不是“学过搜索”，而是“做过搜索系统”。
