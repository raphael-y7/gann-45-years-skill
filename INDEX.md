# Skill 地图 — 江恩华尔街45年

8 张能力卡的全景索引：先看这张表确认该找哪张卡，再按路由入口加载，避免把整本书一次读进来。

## 能力总表

| capability_id | slug | 中文标题 | 重要度 | 去向 |
|---|---|---|---|---|
| `cap.gann-45-years-skill.trade-risk-checklist` | `gann-trade-risk-checklist-skill` | 交易风控与资金管理自检（24条永恒规则） | critical | promoted → 独立 skill |
| `cap.gann-45-years-skill.percentage-levels` | `gann-percentage-levels-skill` | 百分比阻力位与50%中点计算 | high | promoted → 独立 skill |
| `cap.gann-45-years-skill.trend-safe-entry` | `gann-trend-safe-entry-skill` | 趋势确认与最安全买卖点判定 | critical | promoted → 独立 skill |
| `cap.gann-45-years-skill.time-cycle-calendar` | `gann-time-cycle-calendar-skill` | 时间周期变盘日历 | high | promoted → 独立 skill |
| `cap.gann-45-years-skill.swing-charts` | `gann-swing-charts-skill` | 3日图与9点摆动图维护及信号 | high | promoted → 独立 skill |
| `cap.gann-45-years-skill.volume-confirm` | `gann-volume-confirm-skill` | 成交量确认规则（放量见顶/枯竭见底） | medium | router → 路由入口 |
| `cap.gann-45-years-skill.pyramid-profit-protect` | `gann-pyramid-profit-protect-skill` | 金字塔加码与利润保护规程 | high | promoted → 独立 skill |
| `cap.gann-45-years-skill.pair-trade` | `gann-pair-trade-skill` | 错流市多空配对（买强空弱） | medium | router → 路由入口 |

- **promoted（6 张）**：通过五条晋级判据，在 pack 模式下各自独立成 skill，可被 description 直接命中。
- **router（2 张）**：知识验证通过但独立触发意图弱（`volume-confirm`）或来源单薄（`pair-trade`），经来源路由入口 `gann-45-years-skill-router` 到达，不失联。

## 依赖关系

`also_read` 记录的"读完主卡后建议补读"关系（箭头指向补读卡）。下用 capability_id 的末段简称，与上表 `cap.gann-45-years-skill.<简称>` 一一对应：

- `trade-risk-checklist` → `pyramid-profit-protect`、`trend-safe-entry`
- `percentage-levels` → `trend-safe-entry`、`time-cycle-calendar`
- `trend-safe-entry` → `swing-charts`、`percentage-levels`、`trade-risk-checklist`
- `time-cycle-calendar` → `swing-charts`、`trend-safe-entry`
- `swing-charts` → `trend-safe-entry`、`time-cycle-calendar`
- `volume-confirm` → `trend-safe-entry`、`percentage-levels`
- `pyramid-profit-protect` → `trade-risk-checklist`、`trend-safe-entry`
- `pair-trade` → `percentage-levels`、`trend-safe-entry`

从依赖图可以看出两件事：

- `trend-safe-entry` 是全网的中心节点——除它自己之外，其余 7 张卡全部把它列为补读项，因为方向判定是其他一切动作的前置。
- 价格、时间、图表三者串成一条交叉核对链：`percentage-levels` → `time-cycle-calendar`，而 `time-cycle-calendar` 与 `swing-charts` 互为补读。也就是说"这个价位重要"之后要问"时间到没到"，再问"摆动图给什么信号"。

## 加载顺序

1. **先读入口** `SKILL.md`（single 模式是 `single/gann-45-years-skill/SKILL.md`，pack 模式是对应独立 skill 或 `pack/gann-45-years-skill-router/SKILL.md`）。入口里有核心原则与完整路由表，概览类问题读到这里就能回答，不必加载能力卡。
2. **按路由表加载 1 张卡**。任务明确跨域时最多 2 张，先读主卡，再按 `also_read` 补读。
3. **非能力类查询不进卡**：书名/章节/整书概览 → `references/overview.md`；术语 → `references/glossary.md`；规则速查 → `references/cheatsheet.md`；路由表未覆盖的意图先查 `references/capability-index.md`。
4. **都命不中就别硬套**：明确告知超出本书范围。

完整的能力卡正文在 `bundle/cards/`（8 个文件，与 `bundle/verified.yaml` 的 `capabilities` 条目一一对应），编译后的可安装形态在 `single/` 与 `pack/`。
