# 美股 / 港股数据层参考

这是一个面向 agent 的美股与港股数据源参考 skill：按问题挑选合适的数据层和 HTTP 接口，并提醒调用方核对时间、市场、来源和字段。它是参考资料，不是可直接 import 的 Python SDK，也不会替代研究、估值或交易判断。

## 覆盖范围

| 数据层 | 内容 | 主要范围 |
|---|---|---|
| 1. 行情 | 实时或延时报价 | 美股、港股 |
| 2. K 线 | 日、周、月、分钟数据 | 美股、港股，来源因市场不同 |
| 3. 技术指标 | MA / EMA、MACD、RSI、KDJ、布林带 | 基于 OHLCV 的本地计算 |
| 4. 基本面 | 三大报表、关键指标、分析师预期、机构持仓 | 美股、港股，字段按来源不同 |
| 5. 资金流 | 主力、大单、中单、小单的日级数据 | 美股、港股 |
| 6. 期权 | Calls / Puts 及到期日 | 主要为美股 |
| 7. SEC | Filing 列表与 XBRL 财务数据 | 仅美股 |
| 8. 工具 | 股票搜索、新闻、CIK 映射、全市场列表 | 依接口而异 |

端点、代码映射、响应字段和 Python 片段集中在 [references/data-layers.md](references/data-layers.md)。单次查询只读所需层，避免加载或请求全市场数据。

## 使用方法

### 作为 agent skill

将仓库安装到 agent 平台支持的 skills 目录，保持 SKILL.md 和 references/ 位于 skill 根目录。遇到数据需求时先读 SKILL.md，再按需打开 data-layers.md 中对应层。

### 人工查阅或运行参考片段

1. 在 data-layers.md 搜索数据类型和对应 Layer 标题。
2. 按市场选正确的 ticker 格式：美股、港股和东财 SECID / SECUCODE 规则并不相同。
3. 只复制当前任务所需的 helper / endpoint 代码。
4. 安装 requests 后运行需要的 Python 片段：

~~~bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install requests
~~~

5. 记录查询时间、数据自身时间、市场、币种、数据源与失败项；不能把缺失字段或空值当成 0。

## 数据层选择要点

- 报价与 K 线要记录是否实时、延时或历史数据。
- Yahoo Finance 部分接口依赖 cookie / crumb；接口可能变化。
- SEC EDGAR 为美股 Filing / XBRL 参考来源；请求应按 SEC 当前要求设置合适的 User-Agent。
- 期权链参考主要覆盖美股；不要据此假定港股期权也可用。
- 数据源的可用性和字段可能变化。references 中记录的接口检查日期是 2026-05-20，这只是历史记录，运行时必须重新验证。

## 来源与致谢

[references/data-layers.md](references/data-layers.md) 保留原始参考包的作者与来源信息，并链接到上游项目 [simonlin1212/global-stock-data](https://github.com/simonlin1212/global-stock-data)。上游内容的归属与许可应以原项目说明为准；本仓库的公开状态不会替第三方内容授予许可。

## 文件结构

- **SKILL.md**：选择数据层、调用边界和记录要求。
- [references/data-layers.md](references/data-layers.md)：端点说明、市场代码、代码样例和数据源优先级。

## 许可证

当前仓库未附 LICENSE 文件。请同时查看上游参考项目的许可说明；不要仅凭公开可见推定可复制、修改或再分发。
