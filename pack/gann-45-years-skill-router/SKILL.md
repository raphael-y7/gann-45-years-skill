---
name: gann-45-years-skill-router
description: |
  《江恩华尔街45年》来源路由：当请求属于本书方法论但不确定细分能力时进入（如"江恩怎么说成交量""江恩的配对交易"），
  路由到成交量确认、多空配对两张能力卡及全书参考内容；趋势/风控/百分比/时间周期/摆动图/加码六类高频意图
  由对应晋级 Skill 直接承接，不经此路由。
metadata:
  cangjie.generated-by: cangjie-tools v2.5.0
  cangjie.variant: router
  cangjie.bundle-id: bundle.gann-45-years-skill-45-years
  cangjie.capability-count: 8
  cangjie.entrypoint-count: 7
---
# 江恩华尔街45年（45 Years in Wall Street） — 来源路由入口（compact pack）

## 触发与不触发

**适用**：与本书能力域相关的咨询与任务（见下方路由表的意图列）。
**不适用**：
- 不预测市场（给判定规则与确认信号，不给"必定涨跌"结论）
- 不覆盖现代衍生品定价（1949年期权/权证口径仅作原理参考）
- 不提供1949年后美股数据；时间/点位参数需用用户自有市场数据重标定
- 不含江恩角度线/江恩矩阵等本书未包含的工具

## 核心原则（常驻速览，概览类问题读到这里即可回答）

1. 先确认趋势再行动：更高的高点+更高的低点=多头；破3日底/9点摆动极值是趋势变化第一信号
2. 50%是最重要的支撑阻力位：从极限高低价按百分比外推价位网络，中点必算
3. 时间因素重于价格反转：调整时间3周→6~7周→60~65天层级；变盘前有日历窗口可查
4. 资本10等分、单笔风险≤10%、止损单永远跟随且永不撤销
5. 永不摊平、永不对冲、永不让盈利变损失；预期利润≤3~5点不交易
6. 人性（希望/恐惧/延误/过度交易）是最大亏损来源：规则化执行高于主观判断

## 能力路由（先读本表，按意图加载 1 张能力卡）

| 用户意图 | 先读 | 补读/备注 |
|---|---|---|
| 开仓前检查这笔交易的风控是否合规；计算单笔仓位上限与止损位；亏损后复盘违反了哪条纪律；收到追保通知/浮盈后决定止损怎么放 | references/capabilities/gann-trade-risk-checklist-skill.md | 已晋级为独立 Skill `gann-trade-risk-checklist-skill`（已安装时优先直接使用；本卡仅作原文与背景补充） |
| 计算某指数/个股的支撑位与阻力位价位表；计算极限高低价之间的50%中点；判断某价位为何反复出现顶底（汇聚区统计）；判断跌破50%后的下一目标位 | references/capabilities/gann-percentage-levels-skill.md | 已晋级为独立 Skill `gann-percentage-levels-skill`（已安装时优先直接使用；本卡仅作原文与背景补充） |
| 判断当前市场/个股趋势方向（多头/空头/区间）；找最安全的买入点和卖出点及其止损位；评估双底/三重底/顶底互换形态是否成立；判断突破是否有效（5点容差） | references/capabilities/gann-trend-safe-entry-skill.md | 已晋级为独立 Skill `gann-trend-safe-entry-skill`（已安装时优先直接使用；本卡仅作原文与背景补充） |
| 生成未来一段时间的变盘时间窗口日历；判断当前调整/反弹的时间是否到位；判断时间是否"平衡过度"（本次超过前次=转势信号）；用自有市场摆动记录重建时间周期参数 | references/capabilities/gann-time-cycle-calendar-skill.md | 已晋级为独立 Skill `gann-time-cycle-calendar-skill`（已安装时优先直接使用；本卡仅作原文与背景补充） |
| 用日线数据维护3日摆动图并读取信号；维护9点摆动图并判断强弱；评估当前摆动幅度处于历史分布的什么位置（9~21点占50%+）；选择该用月图/周图/日图/摆动图哪一层 | references/capabilities/gann-swing-charts-skill.md | 已晋级为独立 Skill `gann-swing-charts-skill`（已安装时优先直接使用；本卡仅作原文与背景补充） |
| 用成交量确认价格信号的可靠性；判断放量/缩量在顶部区还是底部区的含义 | references/capabilities/gann-volume-confirm-skill.md | references/capabilities/gann-trend-safe-entry-skill.md、references/capabilities/gann-percentage-levels-skill.md |
| 已有盈利持仓时制定加码计划；决定止损跟随到什么位置；判断现在是否是错误时点的加码 | references/capabilities/gann-pyramid-profit-protect-skill.md | 已晋级为独立 Skill `gann-pyramid-profit-protect-skill`（已安装时优先直接使用；本卡仅作原文与背景补充） |
| 在分化/错流行情中同时安排一多一空；预先计算配对组合的最大亏损 | references/capabilities/gann-pair-trade-skill.md | references/capabilities/gann-percentage-levels-skill.md、references/capabilities/gann-trend-safe-entry-skill.md |

**非能力类查询**：
- 书名/作者/章节/整书概览 → references/overview.md
- 术语解释 → references/glossary.md
- 决策规则速查（不需要原文依据时） → references/cheatsheet.md
- 完整意图与关键词索引（本表未覆盖的意图先查这里） → references/capability-index.md

## 加载规则

- 每次任务先读本文件，再按路由表加载 **1** 张能力卡；任务明确跨域时最多加载 2 张。
- 概览/书名类问题不加载能力卡，用「核心原则」与 overview.md 回答。
- 路由表与 capability-index.md 都无法命中的意图，明确告知超出本书范围，不要硬套。

## 边界与判停

- 用户市场数据不足（无历史极限高低点/日线序列）时，先补数再套规则，不猜值
- 规则信号互相矛盾时（如价格破位但时间窗口未到），如实报告矛盾并列出两侧证据，不强行给单边结论
- 涉及"把全部资金投入"类请求，直接触发风控自检卡的红线条款
