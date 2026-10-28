<h1 align="center">江恩华尔街45年 Skill</h1>

<p align="center">中文 | <a href="README.en.md">English</a></p>

一套可直接使用的 AI skill 工具包——把威廉·D·江恩《江恩华尔街45年》里那套"时间、价格、成交量"三因素的可复算规则系统，蒸馏成 8 张可单独触发、也可组合调用的能力卡。

它不是原书摘要，也不是读后感，而是把书中可复用的方法论拆成可触发、可执行、可测试的 skill 模块。

## 这套 skills 能解决什么问题

- 开仓前算不清"这笔该买多少股"：资本 10 等分、单笔风险不超过 10%、股数 = 风险预算 ÷ 每股风险；止损价说不出来时先拒绝给仓位，不猜
- 只知道"这里好像是支撑"，说不出具体价位：从极限最高价 / 极限最低价按固定百分比生成价位表，50% 中点必算，同一小区间挤了几个来源要数出来
- 分不清"更高的高点 + 更高的低点"和"跌多了弹一下"：三层一致性与最安全买点四要素逐项核对，缺一条就报"结构未完成，等待"
- 时间维度全靠感觉：调整时间层级与天数窗口可以提前生成变盘日历，"本次调整时间首次超过前一次"有明确的判定口径
- 3 日图、9 点摆动图到底怎么画、什么才算信号：维护口径（≤2 日的反向运动一律忽略）与"跌破 3 日底 / 穿越 3 日头"的信号定义
- 浮盈后要不要加码、止损跟到哪，亏了要不要"补仓摊低"或"空另一只对冲"：加码指纹与止损序列可生成，而亏损加仓与对冲是原书明令禁止的红线

## 蒸馏了什么

8 张能力卡，按"先守底线、再定位、后进阶"的顺序分成 5 组（slug 与 `bundle/verified.yaml` 的 `capabilities` 逐条对应）：

- **风控纪律**：`gann-trade-risk-checklist-skill`（交易风控与资金管理自检，24 条永恒规则）
- **价格与趋势**：`gann-percentage-levels-skill`（百分比阻力位与 50% 中点计算）、`gann-trend-safe-entry-skill`（趋势确认与最安全买卖点判定）
- **时间与图表**：`gann-time-cycle-calendar-skill`（时间周期变盘日历）、`gann-swing-charts-skill`（3 日图与 9 点摆动图维护及信号）
- **成交量**：`gann-volume-confirm-skill`（成交量确认规则：放量见顶 / 枯竭见底）
- **进阶操作**：`gann-pyramid-profit-protect-skill`（金字塔加码与利润保护规程）、`gann-pair-trade-skill`（错流市多空配对，买强空弱）

## 两种打包模式：single 与 pack

同一套 8 张能力卡，按两种粒度各编译了一次。两者内容完全相同，区别只在"agent 能看到几个入口"。

| | single（单一入口） | pack（compact pack，多入口） |
|---|---|---|
| 可发现入口 | **1 个**：`gann-45-years-skill` | **7 个**：1 个来源路由入口 + 6 个已晋级独立 skill |
| 8 张能力卡放在哪 | 全部在入口的 `references/capabilities/` 里，由入口按路由表按需加载 1–2 张 | 6 张高频卡各自独立成 skill；成交量确认与多空配对这 2 张仍留在 router 的 `references/` 里 |
| 触发方式 | 只有入口的 description 参与匹配，进入后靠路由表分流 | 6 个高频能力可被 description 直接命中，少一跳 |
| 升级维护 | 替换 1 个目录 | 替换 7 个目录 |

pack 里被晋级为独立 skill 的 6 张卡：

- `gann-trade-risk-checklist-skill` — 交易风控与资金管理自检（24 条永恒规则）
- `gann-percentage-levels-skill` — 百分比阻力位与 50% 中点计算
- `gann-trend-safe-entry-skill` — 趋势确认与最安全买卖点判定
- `gann-time-cycle-calendar-skill` — 时间周期变盘日历
- `gann-swing-charts-skill` — 3 日图与 9 点摆动图维护及信号
- `gann-pyramid-profit-protect-skill` — 金字塔加码与利润保护规程

### 该装哪一种

按你的工作方式选，**只装一种**：

| 你的工作方式 | 推荐 | 原因 |
|---|---|---|
| 用 DSH / Codex / Claude Code 等有 skills 目录，希望列表干净 | single | 只占 1 个入口，8 张能力卡一张不少 |
| 日常问题高度集中在"买多少 / 支撑阻力在哪 / 现在能不能买 / 什么时候变盘 / 3 日图什么信号 / 加码止损跟到哪" | pack | 这 6 类正是被晋级的独立 skill，能直接命中 |
| 要分发给多个 agent 或团队，各自按需取用 | pack | 可以只装其中几个独立 skill，不必整包 |
| 只想装一次、不想维护多个目录 | single | 升级时只替换 1 个目录 |

> 两版由同一个 Bundle 编译，能力内容一致。**同时安装会重复触发**，请只装一种。

## 效果示例

### 示例 1：历史最高 120、最低 24，现价 78，回踩到哪能接

**用户问题**

"这票历史最高 120、最低 24，现在 78 块。回踩到哪能接？上面还有多少空间？"

**skill 如何判断**

- 进 `gann-percentage-levels-skill`：先钉起算点——必须是极限最高价 H=120 与极限最低价 L=24；用户给的若是随手挑的拐点，先请其确认，不直接算（这张卡的 B 段把"起算点纪律"列为最常见的误用）
- 生成价位表：中点 (120+24)/2 = 72.00；从 L 向上 +50% = 36.00、+100% = 48.00、+200% = 72.00、+300% = 96.00；从 H 向下 −25% = 90.00、−50% = 60.00、−75% = 30.00
- 汇聚区统计：72.00 同时来自"中点"与"L+200%"两个来源，来源数要单独列出来（原书判定口径是来源数 ≥3 才算汇聚区，这里只有 2 个来源，如实说明达不到）
- 突破判定：这张卡规定价格穿越阻力位需超过容差才算有效（原书 5 点，1 点 = 1 美元的老口径），现代必须先按标的自身波动百分比换算并写明用了哪个数；容差以内一律不确认
- 边界：这张卡只回答"哪里有墙"，不给买卖信号——方向要另读 `gann-trend-safe-entry-skill`，仓位要读 `gann-trade-risk-checklist-skill`

**最终回答示例**

> 先把起算点钉死：120 和 24 是这只票的历史极限高低价吗？如果不是，整张表都要重算，这是这张卡最容易误用的地方。按这两个数：中点 72.00，同时又是 L+200% 位——两个来源撞在同一个价位，这是全书权重最高的单一价位。往下还有 H−50% = 60.00、L+100% = 48.00；往上 H−25% = 90.00、L+300% = 96.00。现价 78 在中点之上、90 之下，属于"仍在阻力区内"，不是有效突破。所以"回踩到哪能接"这个问题，这张卡只能回答"72 是第一个值得盯的位置"，不能回答"到 72 就能买"：跌破 72 且收不住要标极弱，那时下一参考位连同所用口径一起写明。要买卖结论，接着走趋势确认卡核对"更高的高点 + 更高的低点"和最安全买点四要素；要买多少，再走风控卡算仓位。

### 示例 2：亏了 20%，要不要补仓摊低成本

**用户问题**

"我 30 块买的，现在跌到 24，浮亏 20%。要不要再补一笔摊低成本？"

**skill 如何判断**

- 进 `gann-pyramid-profit-protect-skill`：这张卡的执行步骤第 5 条是故障分支——识别到"亏损加仓"意图立即停止并输出禁令（永不均分损失），不给加码方案；B 段另写明本卡只顺利润加、与网格 / 马丁格尔式的越亏越加方向相反
- 转 `gann-trade-risk-checklist-skill`：禁令层里"不摊平（永不均分损失）"与"不对冲"是明列条款，任一条违反就输出"不交易"及违反的条款名称
- 仓位口径：单笔风险额 = 总资本 × 10%；每股风险 = |现价 − 止损价|；股数上限 = 风险额 ÷ 每股风险。用户没给止损价，第一步不是补仓，是把止损价定下来

**最终回答示例**

> 不加。这条在原书里是"永不均分损失"，不是"不太建议"，是禁令；加码卡一识别到亏损加仓就直接停止，不给方案。要算细一点，走风控卡：单笔风险上限是总资本的 10%，每股风险等于现价减止损价，股数上限等于风险额除以每股风险——你现在连止损价都没定，所以第一步不是补仓，而是先把止损价写下来。补仓确实能把平均成本压低，但同时放大仓位、放大最大亏损，等于把"资本 10 等分、单笔不超 10%"这条红线一起推翻。原书对这类情况的处理是：先把亏损归因到自己，回溯 24 条定位违反了哪一条并记录下来，然后离场，不犯第二次。另外提醒一句，加码卡只处理"已有盈利持仓的加码与止损跟随"，永不向亏损仓加码，这与网格 / 马丁格尔式的越亏越加正好相反，两套体系不要混用。

## 这些 skill 是怎么生成出来的

这套 skill 使用 **[cangjie-skill](https://github.com/kangarooking/cangjie-skill)** 的 RIA-TV++ 流水线生成，整个流程分六个阶段：

1. **整书理解（Adler 分析）**——用 Mortimer Adler 的分析阅读法，对全书做结构、解释、批判、应用四步拆解，先定下"哪一层可用、哪一层只能当案例"
2. **并行提取**——同时派多个专项提取器（框架、原则、案例、反例、术语），从原文中提取候选方法论单元
3. **三重验证筛选**——每个候选必须通过三项检验：书内至少有 2 处独立佐证（跨域）、能回答书中未明说的新问题（预测力）、不是常识（独特性）
4. **RIA++ 构造**——按 R（原文引用）/ I（用自己的话重写）/ A1（书中案例）/ A2（未来触发场景）/ E（可执行步骤）/ B（边界与盲点）六个维度结构化
5. **Zettelkasten 链接**——找出能力卡之间的依赖、对比、组合关系，生成能力索引与路由表
6. **触发与输出测试**——为每张卡设计触发盲测题（含诱饵题：该触发时要触发，不该触发时要沉默）与输出评测场景，未通过的卡回炉重做，回炉后再做回归验证

这本书的蒸馏还多一层取舍：全书最耐用的是"风控纪律层"（24 条永恒规则、资本 10 等分、止损体系），而"历史叙事层"（大炒家兴衰、战争循环、对后市的推演）只作为案例与背景保留，不编译成可执行能力。价格、时间、图表三层的方法可迁移，但其中的绝对点位参数是原书时代的道指尺度，因此每张卡都把"必须按标的自身波动重标定并声明口径"写进了边界段。

## 测试与验证

本仓库把评测材料随 skill 一起发布：触发用例见各 skill 目录下的 `test-prompts.json`，逐项评分与修复记录见仓库根目录的 `test-results.md`——包括没做到的部分，不是只留通过记录。测试宿主为 ZCode / GLM-5.3，盲测由未参与蒸馏、看不到预期答案与断言的独立子智能体执行。

- **触发精度盲测**：32 条 prompt × 8 项能力，完全命中 30 / 32，边缘可接受 2 条（t21、t22），**错误激活 0**；其中 8 条跨能力诱饵全部正确避开
- **输出评测**：8 项能力 × 正常 / 边界两个场景，共 16 个场景，**16 / 16 全过，0 失败**
- **带卡 vs 无卡对照**：16 个场景每个都跑带卡与不带卡两版，报告归纳出 5 处关键差异——卡在哪几处交付了方法本体（无卡版本把 3 日图误解成"跌破前三日最低点"的滚动口径、把"5 个点"误读成 5%），以及计算类题目与基线算术同准
- **修复记录**：t21 暴露近邻歧义后，摆动图卡的 description 增补"只产出图表信号，不做开仓决策与仓位"；除此之外无其他回炉项
- **如实说明**：t22（"用 3 日均线分析"）判官判为无匹配能力，属于防御性合理，理想行为是触发摆动图卡并纠正口径（均线 ≠ 摆动图），本次不判失败但已记录在案

## 仓库结构

```text
gann-45-years-skill/
├── README.md              ← 你正在看的
├── README.en.md           ← English version
├── LICENSE                ← MIT
├── BOOK_OVERVIEW.md       ← 阶段 0 产出：全书 Adler 分析
├── DIGEST.md              ← 阶段 5 产出：面向读者的整书精华长文
├── INDEX.md               ← 阶段 3 产出：skill 总览 + 依赖关系
├── verified.md            ← 通过三重验证的 8 个单元
├── TEST_SUMMARY.md        ← 阶段 4 产出：压力测试摘要
├── CANGJIE_ADAPTATION.md  ← 仓颉适配说明
├── GITHUB_REPO.md         ← 仓库元数据
├── test-results.md        ← 测试结果记录
├── candidates/            ← 阶段 1 产出：原始候选池
│   ├── frameworks.md      ← 框架与方法候选
│   ├── principles.md      ← 原则 / 规则 / 计算候选
│   ├── cases.md           ← 书中案例候选
│   ├── counter-examples.md← 反例与边界候选
│   └── glossary.md        ← 术语候选
├── rejected/              ← 阶段 1.5 产出：被淘汰的单元 + 原因
├── bundle/                ← 编译事实源
│   ├── verified.yaml      ← 能力元数据、判据与去向
│   ├── cards/             ← 能力卡源文件（六段结构）
│   └── book/              ← overview.md + glossary.md
├── single/                ← single 模式（1 个入口 + 全部能力卡）
│   └── gann-45-years-skill/SKILL.md  ← 入口：触发 + 路由表 + 加载规则
└── pack/                  ← pack 模式（1 个路由入口 + 6 个晋级 skill）
    └── */SKILL.md         ← 7 个 skill，每个附带 test-prompts.json
```

## 如何使用

先把仓库克隆下来：

```bash
git clone https://github.com/raphael-y7/gann-45-years-skill.git
```

### 装 single（推荐先试这个）

```bash
# macOS / Linux
cp -r gann-45-years-skill/single/gann-45-years-skill ~/.agents/skills/
```

```powershell
# Windows
Copy-Item -Recurse .\gann-45-years-skill\single\gann-45-years-skill "$env:USERPROFILE\.agents\skills\"
```

### 装 pack

只复制含 `SKILL.md` 的目录，不要把 `pack/` 下的两个 json 一起拷进 skills 目录：

```bash
# macOS / Linux
cd gann-45-years-skill/pack
cp -r gann-45-years-skill-router \
      gann-trade-risk-checklist-skill \
      gann-percentage-levels-skill \
      gann-trend-safe-entry-skill \
      gann-time-cycle-calendar-skill \
      gann-swing-charts-skill \
      gann-pyramid-profit-protect-skill ~/.agents/skills/
```

```powershell
# Windows
$pack = ".\gann-45-years-skill\pack"
$dest = "$env:USERPROFILE\.agents\skills"
@('gann-45-years-skill-router','gann-trade-risk-checklist-skill','gann-percentage-levels-skill','gann-trend-safe-entry-skill','gann-time-cycle-calendar-skill','gann-swing-charts-skill','gann-pyramid-profit-protect-skill') |
  ForEach-Object { Copy-Item -Recurse -LiteralPath (Join-Path $pack $_) -Destination $dest }
```

> `~/.agents/skills` 是 DSH 的 skill 目录；用别的 agent 时换成它自己的 skills 目录即可（例如 Claude Code 是 `~/.claude/skills`）。

### 怎么确认装好了

装完问一句"这笔交易我该买多少股、止损放哪"，看 agent 是否直接进入 24 条规则的仓位计算（风险预算 ÷ 每股风险，止损没定就先反问），而不是给你一段泛泛的仓位建议。装的是 single 时，它会先读入口再按路由表进能力卡；装的是 pack 时，对应能力会被直接命中。

## 来源

- 《江恩华尔街45年》（45 Years in Wall Street）威廉·D·江恩 著

## 声明

本仓库只发布蒸馏后的 skill、索引与规则速查材料，不包含原书 PDF、EPUB、OCR 文件、截图或全书转写稿。能力卡中出现的原文引用仅用于标注方法论出处和保持可审计性。

书中所有数字判据（3~5 点止损、5 点突破容差、9 点摆动阈值、调整天数窗口、百分比档位等）都是案例与经验归纳，原书未提供统计回测背书，且全部基于原书时代的道指点位尺度，使用时需按标的自身波动重标定并声明所用口径。本仓库内容不构成投资建议。

## License

[MIT](./LICENSE)
