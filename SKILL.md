---
name: global-stock-data
description: 获取美股/港股报价、K线、财务、期权链或 SEC 数据的备选 HTTP 数据层；明确需要这些数据且当前专用数据源不足时使用，不接管普通个股分析。
metadata:
  origin: custom
  version: '1.0'
---

# 美股港股数据工具

这是数据获取能力，分析与报告交给当前任务或对应研究 skill。端点与示例代码保存在 [data-layers.md](references/data-layers.md)，保留原作者与来源信息。

按需读取共用 Helper、市场代码规则和对应层：Layer 1 报价、Layer 2 K线、Layer 3 指标、Layer 4 财务、Layer 5 资金流、Layer 6 期权、Layer 7 SEC、Layer 8 搜索。不要为单一价格查询加载所有代码或遍历全市场。

记录查询时间、数据时间、市场/币种、来源与失败项。参考中的可用性记录有历史日期；运行时验证接口和字段，失败再按该层备选源降级，不能把空值当零。批量拉取按全局采集分工与增量规则执行。
