# 搜索架构师前 90 天任务面板

更新时间：2026-04-11

这份文档只做一件事：让你在前 90 天直接开干。

范围只覆盖前 3 个月，因为这一段最关键。前 90 天如果没有把评估、IR 基础、POI 数据建模、数据治理这几个底层动作做实，后面学粗排、精排、模型、架构都会飘。

默认每周投入 `10-15h`。每周必须留下：

- 1 份笔记
- 1 个实验
- 10 条 badcase 分析
- 1 个结构化交付物

## 第 1 月：评估体系与 badcase 基线

## 第 1 周：建立问题地图

本周目标：

- 先把当前搜索问题看清楚，不要急着改策略。

任务清单：

- 梳理当前搜索主链路：`query -> recall -> rank -> result`
- 盘点已有数据：query 日志、点击日志、POI 数据、索引字段
- 抽样 `50-100` 条 query，按直觉先做初步归类
- 起草 query taxonomy v1：`brand/address/category/nearby/route/ambiguous/landmark`

本周交付物：

- 当前链路草图
- query taxonomy v1
- 数据资产清单

验收标准：

- 你能说出当前系统最少 5 类问题
- 你能把 30 条 query 归到明确 bucket

常见风险：

- 一上来就想调排序
- 没有先搞清楚 query 类型

## 第 2 周：建立标注规范

本周目标：

- 让“好结果”有统一标准。

任务清单：

- 选 `200-300` 条代表性 query
- 按 bucket 分布抽样
- 定义 4 级相关性标准：`3/2/1/0`
- 为每个等级写具体例子
- 建立 judgment sheet

本周交付物：

- relevance guideline v1
- judgment set v1

验收标准：

- 同一条 query，你自己一周后复标结果基本一致
- 每个 bucket 都有样本，不是只标品牌词

常见风险：

- 标注规则过于抽象
- 只标最简单 query

## 第 3 周：跑 baseline 评估

本周目标：

- 拿到第一版客观基线。

任务清单：

- 跑当前搜索结果 TopK 快照
- 计算 `Recall@10 / MRR / NDCG@5 / NDCG@10`
- 按 bucket 输出分桶指标
- 找出 Top bad buckets

本周交付物：

- baseline 评估报告
- 分桶指标表

验收标准：

- 你能明确说出当前最差的 2-3 类 query
- 指标可重复计算，不是手工感受

常见风险：

- 只看整体指标，不看分桶
- 不保留结果快照，无法复现

## 第 4 周：建立 badcase 归因体系

本周目标：

- 让 badcase 能回到链路，不再停留在“结果不对”。

任务清单：

- 建立 badcase 分类：`data/query/recall/rank/geo/system`
- 抽 `50` 个 badcase 做归因
- 每个 badcase 至少写一级归因和二级归因
- 总结高频问题 Top5

本周交付物：

- badcase 库 v1
- badcase 周报 v1

验收标准：

- 至少 80% 的 badcase 有清晰归因
- 你能说出哪个环节最值得优先投入

常见风险：

- 只写现象，不写根因
- 所有问题都归到“排序不好”

## 第 2 月：IR、Lucene、检索 baseline

## 第 5 周：极简倒排与 BM25

本周目标：

- 把检索原理真正内化。

任务清单：

- 手写极简倒排 demo
- 用自己的 POI 样本做 token -> postings
- 理解 TF、IDF、长度归一化
- 实现最小 BM25 打分

本周交付物：

- 倒排 demo
- BM25 实验笔记

验收标准：

- 你能不用搜索引擎术语，自己讲明白倒排和 BM25

常见风险：

- 只背概念，不动手

## 第 6 周：字段权重与 analyzer

本周目标：

- 知道为什么 `name/alias/address/category` 不能混成一锅。

任务清单：

- 设计字段：`name/alias/address/category/brand`
- 比较不同 analyzer：精确、分词、前缀
- 比较不同字段 boost
- 记录典型 badcase 的字段命中情况

本周交付物：

- 字段设计说明
- analyzer 对比报告

验收标准：

- 你能说明每个字段为什么需要自己的索引策略

常见风险：

- 想用一套 analyzer 解决全部问题

## 第 7 周：explain、profile 与分数拆解

本周目标：

- 不再把“分数异常”当黑盒。

任务清单：

- 选 `10-20` 个 badcase
- 跑 explain
- 拆 term 命中、字段命中、长度归一化、boost 影响
- 跑 profile 看查询耗时

本周交付物：

- explain 分析文档
- profile 分析文档

验收标准：

- 你能解释至少 10 个 case 为什么排成现在这样

常见风险：

- 只看结果，不看 explain
- 只看相关性，不看耗时

## 第 8 周：geo 检索 baseline

本周目标：

- 让空间约束进入基线系统。

任务清单：

- 加入 `geo_point`
- 实现 geo filter、geo sort、distance feature
- 比较纯文本排序 vs 加距离特征
- 分析 nearby 类 query 的收益与副作用

本周交付物：

- geo baseline
- nearby 初步实验报告

验收标准：

- 你能说明什么时候该 filter，什么时候该 score

常见风险：

- 用硬过滤误伤结果
- 让距离完全压过文本相关性

## 第 3 月：POI 数据建模与数据治理

## 第 9 周：POI schema 设计

本周目标：

- 定义统一实体模型。

任务清单：

- 设计 `poi_id/source_id/canonical_id`
- 设计核心字段：名称、别名、地址、类目、品牌、营业状态、坐标、更新时间
- 设计层级字段：城市、区县、商圈、道路、门牌
- 设计缺省值与空值策略

本周交付物：

- POI schema v1
- 字段字典 v1

验收标准：

- 新数据接入时，你知道该放到哪个字段

常见风险：

- 只按当前索引字段设计，不按长期实体治理设计

## 第 10 周：多源融合策略

本周目标：

- 定义“多个来源来了怎么办”。

任务清单：

- 盘点数据源优先级
- 设计字段冲突处理策略
- 设计时间优先级与可信度优先级
- 定义状态冲突：闭店、搬迁、重命名

本周交付物：

- merge policy v1
- source priority 表

验收标准：

- 你能举例说明两条冲突 POI 怎么合并

常见风险：

- 默认最新就是最好
- 不区分字段级可信度

## 第 11 周：去重策略

本周目标：

- 解决同名、近邻、连锁门店的实体冲突。

任务清单：

- 定义 duplicate case：同名同点、同名近点、别名匹配、品牌门店
- 建规则 baseline
- 抽样看错合并和漏合并
- 设计下一阶段可模型化的特征

本周交付物：

- duplicate policy v1
- 去重样本集

验收标准：

- 你能明确说出哪些 case 可以规则做，哪些以后要模型做

常见风险：

- 看到同名就合
- 不区分品牌主实体和门店实体

## 第 12 周：质量分与 90 天复盘

本周目标：

- 给实体打可信度分，并做第一阶段总复盘。

任务清单：

- 设计质量分维度：名称完整度、地址完整度、坐标可信度、营业状态可信度、类目可信度
- 给一批 POI 打质量分
- 复盘前 90 天产出
- 制定第 4-6 月进入 Query 理解与 Suggest 的准备项

本周交付物：

- quality score v1
- 前 90 天复盘报告
- 下一阶段准备清单

验收标准：

- 你能把当前主要短板明确排优先级
- 你已经具备进入 Query 理解与 Suggest 阶段的基础

常见风险：

- 没有做阶段复盘就直接冲下一个模块

## 前 90 天结束时你必须具备的成果

- 1 套 query taxonomy
- 1 套 judgment set
- 1 套 baseline 指标
- 1 套 badcase 归因体系
- 1 个 BM25 / geo baseline
- 1 套 POI schema
- 1 套 merge policy
- 1 套 duplicate policy
- 1 套 quality score v1

## 前 90 天结束时你必须能回答的问题

- 当前系统最差的是哪几类 query
- 这些问题分别属于数据、query、召回、排序、geo 哪一层
- 为什么某个结果会排第一
- 为什么 nearby 不能只看文本相关性
- 为什么同名 POI 不能简单按字符串合并
- 为什么质量分会影响后续召回和排序

## 使用建议

这份任务面板要和下面几份文档一起用：

- 用 [search-architect-ultimate-roadmap.md](/Users/levi/develop/project/search/search/doc/search-architect-ultimate-roadmap.md) 看长期方向
- 用 [search-architect-24-month-execution-plan.md](/Users/levi/develop/project/search/search/doc/search-architect-24-month-execution-plan.md) 看完整节奏
- 用 [map-search-templates.md](/Users/levi/develop/project/search/search/doc/map-search-templates.md) 记录每周过程

不要跳周执行。前 90 天最怕的不是学得慢，而是基础没打实就提前做模型和复杂架构。
