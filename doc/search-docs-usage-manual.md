# 搜索学习资料使用手册

更新时间：2026-04-11

这份手册告诉你：这套文档该怎么用，先看什么，什么时候切到下一份，如何避免“文档很多，但最后没有真正执行”。

## 1. 这套文档解决什么问题

这套资料不是只给你知识点，而是给你 4 层东西：

1. 方向：你最终要成长到哪里
2. 路线：你按什么顺序学习
3. 执行：你每周每月具体做什么
4. 落地：你如何做实验、做项目、做方案、做复盘

## 2. 先认识每份文档的定位

- [map-search-senior-learning-roadmap.md](/Users/levi/develop/project/search/search/doc/map-search-senior-learning-roadmap.md)
  作用：总览版，适合先建立地图搜索整体认知。

- [poi-search-principal-learning-roadmap.md](/Users/levi/develop/project/search/search/doc/poi-search-principal-learning-roadmap.md)
  作用：负责人版，补齐 POI 数据、Suggest、召回路由、粗排精排、训练闭环。

- [search-architect-ultimate-roadmap.md](/Users/levi/develop/project/search/search/doc/search-architect-ultimate-roadmap.md)
  作用：最高目标版，面向搜索架构师，加入分布式架构、索引构建、性能、成本、团队方法论。

- [search-architect-24-month-execution-plan.md](/Users/levi/develop/project/search/search/doc/search-architect-24-month-execution-plan.md)
  作用：执行版，按月按周推进，不让路线停留在概念上。

- [search-architect-first-90-days-task-board.md](/Users/levi/develop/project/search/search/doc/search-architect-first-90-days-task-board.md)
  作用：起步版，把前 90 天拆到每周任务、交付物、验收标准和风险，适合立刻开干。

- [search-architect-reading-experiments-and-teardowns.md](/Users/levi/develop/project/search/search/doc/search-architect-reading-experiments-and-teardowns.md)
  作用：输入与实操清单，告诉你读什么、做什么实验、拆什么源码。

- [map-search-practice-projects.md](/Users/levi/develop/project/search/search/doc/map-search-practice-projects.md)
  作用：项目版，帮你把路线落成系统。

- [map-search-templates.md](/Users/levi/develop/project/search/search/doc/map-search-templates.md)
  作用：模板版，记录 badcase、评估、周报、实验、方案。

- [map-search-tech-design-template.md](/Users/levi/develop/project/search/search/doc/map-search-tech-design-template.md)
  作用：方案版，做专项时强制你说清目标、评估、风险、回滚。

- [map-search-self-assessment-and-interview-bank.md](/Users/levi/develop/project/search/search/doc/map-search-self-assessment-and-interview-bank.md)
  作用：自测版，用来检查你有没有真的掌握。

## 3. 推荐使用顺序

如果你刚开始：

1. 先读 [map-search-senior-learning-roadmap.md](/Users/levi/develop/project/search/search/doc/map-search-senior-learning-roadmap.md)
2. 再读 [poi-search-principal-learning-roadmap.md](/Users/levi/develop/project/search/search/doc/poi-search-principal-learning-roadmap.md)
3. 最后读 [search-architect-ultimate-roadmap.md](/Users/levi/develop/project/search/search/doc/search-architect-ultimate-roadmap.md)

如果你已经在做真实 POI 搜索开发：

1. 直接读 [poi-search-principal-learning-roadmap.md](/Users/levi/develop/project/search/search/doc/poi-search-principal-learning-roadmap.md)
2. 同时读 [search-architect-ultimate-roadmap.md](/Users/levi/develop/project/search/search/doc/search-architect-ultimate-roadmap.md)
3. 然后按 [search-architect-24-month-execution-plan.md](/Users/levi/develop/project/search/search/doc/search-architect-24-month-execution-plan.md) 执行

如果你的目标就是搜索架构师：

1. 用 [search-architect-ultimate-roadmap.md](/Users/levi/develop/project/search/search/doc/search-architect-ultimate-roadmap.md) 定义上限
2. 先按 [search-architect-first-90-days-task-board.md](/Users/levi/develop/project/search/search/doc/search-architect-first-90-days-task-board.md) 起步
3. 再用 [search-architect-24-month-execution-plan.md](/Users/levi/develop/project/search/search/doc/search-architect-24-month-execution-plan.md) 管长期节奏
4. 用 [search-architect-reading-experiments-and-teardowns.md](/Users/levi/develop/project/search/search/doc/search-architect-reading-experiments-and-teardowns.md) 管输入和实验
5. 用项目手册、模板、方案模板把过程沉淀下来

## 4. 每周怎么用

建议固定节奏：

- 周一：按路线图确定本周主题
- 周二：读资料和源码
- 周三：做最小实验
- 周四：分析 badcase 和日志
- 周五：写周报和结论
- 周末：决定下周是否进入下一阶段

每周至少要留下 4 个东西：

- 1 篇笔记
- 1 个实验
- 10 条 badcase 分析
- 1 页结论

## 5. 每月怎么用

每月固定做 5 件事：

1. 对照执行计划检查是否完成当月 4 周任务
2. 跑一轮离线评估
3. 更新 badcase 分类分布
4. 输出一份月度复盘
5. 决定是否进入下一月主题

如果这 5 件事没做完，不要急着看下一个高级模块。

## 6. 什么时候切到下一份文档

从总览版切到负责人版：

- 当你已经知道基础概念，但开始遇到 POI 数据、Suggest、召回、排序等真实问题时

从负责人版切到架构师版：

- 当你开始关心索引构建、训练闭环、性能、稳定性、成本、灰度和回滚时

从路线图切到执行计划：

- 当你已经明确方向，准备开始按月推进时

从执行计划切到前 90 天任务面板：

- 当你已经准备立即开工，需要一份不需要再自己拆分的起步清单时

从执行计划切到资料/实验清单：

- 当你知道这周做什么，但不知道看什么、拆什么、实验什么时

## 7. 怎么避免学习漏项

最常见的漏项有：

- 只学相关性，不学数据治理
- 只学排序，不学召回
- 只学模型，不学业务重排
- 只学算法，不学索引构建和服务架构
- 只看论文，不做实验
- 只做实验，不写总结

避免方式：

- 每个月都对照 `数据 / Query / 召回 / 排序 / 评估 / 架构` 六个维度自查一次
- 每次 badcase 都强制归因到链路
- 每个阶段都要留下系统级交付物，而不是只有笔记

## 8. 遇到真实工作问题时怎么查文档

如果你遇到：

- `数据融合、清洗、去重`
  去看 [poi-search-principal-learning-roadmap.md](/Users/levi/develop/project/search/search/doc/poi-search-principal-learning-roadmap.md) 和 [search-architect-ultimate-roadmap.md](/Users/levi/develop/project/search/search/doc/search-architect-ultimate-roadmap.md)

- `Suggest、别名、意图识别`
  去看负责人版路线和资料/实验清单

- `粗排、精排、业务重排`
  去看负责人版路线、架构师路线、项目手册

- `地址搜索、nearby、along-route`
  去看负责人版路线、架构师路线、源码拆解清单

- `训练样本、偏差校正、A/B`
  去看架构师路线和资料/实验清单

- `索引构建、时效性、延迟、成本`
  直接去看架构师路线和执行计划后半段

- `我现在这周到底做什么`
  先去看 [search-architect-first-90-days-task-board.md](/Users/levi/develop/project/search/search/doc/search-architect-first-90-days-task-board.md)

## 9. 最推荐的使用方式

最好的用法不是把这些文档从头读到尾，而是：

1. 先定目标：你现在在哪个阶段
2. 再定主题：你本月要解决哪类问题
3. 再定输入：你要读哪些资料、拆哪些源码
4. 再定输出：你本周要交付什么
5. 最后复盘：你这次收益来自哪里，短板还在哪

## 10. 一句话版使用原则

- 路线图负责定方向
- 执行计划负责定节奏
- 资料清单负责定输入
- 项目手册负责定系统
- 模板负责定沉淀
- 技术方案模板负责定负责人标准

如果你能连续 12 到 24 个月按这个方式执行，这套文档才会真正把你推向搜索架构师，而不是停留在“知道很多名词”。
