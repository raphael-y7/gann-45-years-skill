<h1 align="center">Gann 45 Years Skill</h1>

<p align="center"><a href="README.md">中文</a> | English</p>

An AI skill pack for immediate use — it distills the reproducible rule system of "time, price and volume" in *45 Years in Wall Street* into 8 capability cards that can be triggered individually or combined.

It is not a book summary, nor a reading response — it breaks the reusable methodology in the book into skill modules that can be triggered, executed and tested.

## What these skills solve

- You cannot work out how many shares to buy before entering: capital split into 10 equal parts, single-trade risk capped at 10%, shares = risk budget ÷ per-share risk — and when you cannot state a stop price, the skill refuses to size the position instead of guessing
- You only know "this looks like support" but cannot name a price: build the price table from the extreme high and extreme low by fixed percentages, always compute the 50% midpoint, and count how many sources pile into the same narrow band
- You cannot tell "higher high plus higher low" from "a bounce after a fall": the three-layer consistency check and the four-element safest-entry sequence are verified item by item, and one missing element yields "structure incomplete, wait"
- Your time dimension is pure feeling: the adjustment-time hierarchy and day windows can be turned into a forward-looking turn-date calendar, and "this move has lasted longer than the previous one" has an explicit test
- You do not know how a 3-day chart or a 9-point swing chart is actually maintained, or what counts as a signal: the maintenance convention (ignore any counter-move of 2 days or less) and the "break of the 3-day bottom / crossing of the 3-day top" definitions are spelled out
- Whether to add to a winner, where the trailing stop goes, and whether to "average down" a loser or "hedge" it with a short: the pyramiding fingerprint and stop sequence are generated, while averaging down and hedging are hard red lines in the book

## What was distilled

8 capability cards, in five groups ordered "hold the floor first, locate second, advance last":

- **Risk discipline**: `trade-risk-checklist` (pre-trade risk and money-management self-check, the 24 timeless rules)
- **Price and trend**: `percentage-levels` (percentage resistance levels and the 50% midpoint), `trend-safe-entry` (trend confirmation and the safest buy/sell point)
- **Time and charts**: `time-cycle-calendar` (time-cycle turn-date calendar), `swing-charts` (3-day chart and 9-point swing chart maintenance and signals)
- **Volume**: `volume-confirm` (volume confirmation: climax tops, exhaustion bottoms)
- **Advanced operations**: `pyramid-profit-protect` (pyramiding and profit protection), `pair-trade` (long/short pairing in a cross-current market — buy the strong, short the weak)

## Two packaging modes: single and pack

The same 8 capability cards are compiled twice, at two granularities. The content is identical; the only difference is how many entries an agent can discover.

| | single (one entry) | pack (compact pack, multiple entries) |
|---|---|---|
| Discoverable entries | **1**: `gann-45-years-skill` | **7**: one source router + 6 promoted standalone skills |
| Where the 8 cards live | All inside the entry's `references/capabilities/`, loaded 1–2 at a time by the router table | 6 high-frequency cards become standalone skills; the other 2 (volume confirmation, pair trading) stay in the router's `references/` |
| Triggering | Only the entry description participates in matching; routing happens after entry | The 6 high-frequency capabilities are matched directly, one hop fewer |
| Upgrades | Replace 1 directory | Replace 7 directories |

The 6 cards promoted to standalone skills in the pack:

- `gann-trade-risk-checklist-skill` — pre-trade risk and money-management self-check (24 timeless rules)
- `gann-percentage-levels-skill` — percentage resistance levels and the 50% midpoint
- `gann-trend-safe-entry-skill` — trend confirmation and the safest buy/sell point
- `gann-time-cycle-calendar-skill` — time-cycle turn-date calendar
- `gann-swing-charts-skill` — 3-day chart and 9-point swing chart maintenance and signals
- `gann-pyramid-profit-protect-skill` — pyramiding and profit protection

### Which one to install

Pick by the way you work, and **install only one**:

| How you work | Recommended | Why |
|---|---|---|
| You use DSH / Codex / Claude Code with a skills directory and want a clean list | single | Takes 1 slot, loses none of the 8 cards |
| Your daily questions concentrate on "how much to buy / where is support / can I buy now / when does it turn / what does the 3-day chart say / where does the trailing stop go" | pack | Those 6 are exactly the promoted standalone skills, matched directly |
| You distribute to several agents or teammates who pick what they need | pack | They can install only the standalone skills they want |
| You want to install once and maintain one directory | single | Upgrades replace a single directory |

> Both builds come from the same bundle and carry identical capabilities. **Installing both will double-trigger**, so pick one.

## Examples

### Example 1: an all-time high of 120, an all-time low of 24, price now 78 — where can I buy the pullback?

**User question**

"This stock's all-time high is 120 and its all-time low is 24. It trades at 78 now. Where can I buy the pullback, and how much room is left above?"

**How the skill reasons**

- Enter `percentage-levels`: pin the base points first — they must be the extreme high H=120 and the extreme low L=24; if the user offers an arbitrary swing point, ask for confirmation instead of computing
- Build the price table: midpoint (120+24)/2 = 72.00; up from L: +50% = 36.00, +100% = 48.00, +200% = 72.00, +300% = 96.00; down from H: −25% = 90.00, −50% = 60.00, −75% = 30.00
- Confluence count: 72.00 comes from both "midpoint" and "L+200%", so the source count must be reported separately
- Breakout test: the book's confirmation tolerance is 5 points (1 point = 1 dollar in the old scale); in a modern market it must be re-scaled to the instrument's own volatility percentage and the convention stated — anything inside the tolerance is not confirmed
- Boundaries: this card only answers "where are the walls", never gives buy or sell signals — direction goes to `trend-safe-entry`, position size to `trade-risk-checklist`

**Sample answer**

> Pin the base points first: are 120 and 24 really this stock's extreme high and low? If not, the whole table has to be rebuilt — that is the most common misuse of this card. With those two numbers: the midpoint is 72.00, and it is also the L+200% level, two sources landing on the same price, which is the single most important level in the book. Below it there is H−50% = 60.00 and L+100% = 48.00; above it H−25% = 90.00 and L+300% = 96.00. At 78 the price sits above the midpoint and below 90, which is "still inside the resistance zone", not a valid breakout. So on "where can I buy the pullback", this card can only answer "72 is the first level worth watching" — not "72 is a buy". A break below 72 that fails to recover must be flagged as very weak, and at that point the next reference level is reported together with the convention used. For an actual buy or sell decision, continue to the trend card and check "higher high plus higher low" against the four-element safest-entry sequence; for position size, continue to the risk card.

### Example 2: down 20% — should I average down?

**User question**

"I bought at 30, it is 24 now, down 20%. Should I add and lower my average cost?"

**How the skill reasons**

- Enter `pyramid-profit-protect`: its failure branch states that an "add to a losing position" intent must stop the flow immediately and output the prohibition (never average a loss), with no pyramiding plan offered
- Switch to `trade-risk-checklist`: among the 24 timeless rules, #13 "never average a loss" and #22 "never hedge"; violating any one of them means the output is "do not trade" plus the violated rule number
- Position arithmetic: single-trade risk = total capital × 10%; per-share risk = |price − stop|; share cap = risk budget ÷ per-share risk. The user gave no stop price, so the first step is not adding — it is writing down the stop

**Sample answer**

> No. In the book this is timeless rule #13, "never average a loss" — not a mild suggestion but a prohibition, and the pyramiding card's failure branch stops immediately once it detects averaging down. To go further, use the risk card: single-trade risk is capped at 10% of total capital, per-share risk equals price minus stop, and the share cap equals the risk budget divided by per-share risk — you have not set a stop yet, so the first step is to write the stop down, not to add. Adding does lower your average cost, but it also enlarges the position and the maximum loss, which overthrows the "capital in 10 equal parts, never more than 10% per trade" red line. The book's handling of this situation: attribute the loss to yourself first, walk back through the 24 rules to find which one you broke, record it, then exit — and do not repeat it. One more note: the pyramiding card only handles adding to an existing winner with a trailing stop, always in the direction of profit, never into a loss. That is the exact opposite of grid or martingale-style averaging down, so do not mix the two systems.

## How these skills were generated

These skills were produced with the **[cangjie-skill](https://github.com/kangarooking/cangjie-skill)** RIA-TV++ pipeline, in six stages:

1. **Whole-book comprehension (Adler analysis)** — apply Mortimer Adler's analytical reading method to the book: structure, interpretation, criticism, application, settling up front which layer is usable and which can only serve as illustration
2. **Parallel extraction** — several specialized extractors (frameworks, principles, cases, counter-examples, terminology) mine candidate methodology units from the source text
3. **Triple verification** — every candidate must pass three checks: at least two independent in-book supports (cross-domain), the ability to answer questions the book never explicitly addresses (predictive power), and not being common sense (distinctiveness)
4. **RIA++ construction** — structure each unit along R (quotation) / I (restatement in own words) / A1 (in-book case) / A2 (future trigger scenario) / E (executable steps) / B (boundaries and blind spots)
5. **Zettelkasten linking** — map dependencies, contrasts and combinations between cards, producing the capability index and routing table
6. **Trigger and output testing** — write trigger blind tests (including decoy questions: fire when they should, stay silent when they should not) and output evaluation scenarios for every card; failing cards go back for rework and are re-verified afterwards

This book needed one extra judgment call: the most durable layer is the risk-discipline layer (the 24 timeless rules, capital in 10 equal parts, the stop-loss system), while the historical-narrative layer (the rise and fall of big operators, war cycles, forecasts about the future) is kept only as case material and background, never compiled into an executable capability. The price, time and chart layers do transfer, but their absolute point values belong to the index scale of the book's own era, so every card carries "re-scale to the instrument's own volatility and state the convention" in its boundary section.

## Testing and verification

This repository publishes the evaluation material from the audit directory alongside the skills: `evals/` holds the trigger blind-test cases plus the output-evaluation tasks and fixed assertions, and `test-results.md` is the item-by-item scoring and repair log — including what did not work, not just the passes. The test host was ZCode / GLM-5.3, and the blind tests were run by an independent sub-agent that took no part in the distillation and never saw the expected answers or assertions.

- **Trigger precision**: 32 prompts × 8 capabilities — 30 / 32 exact hits, 2 acceptable edge cases (t21, t22), **0 false activations**; all 8 cross-capability decoys were correctly avoided
- **Output evaluation**: 8 capabilities × normal / boundary scenarios = 16 scenarios, **16 / 16 passed, 0 failures**
- **Skill vs no-skill control**: every one of the 16 scenarios was run both with and without the cards, and the report distils 5 key differences — where the cards delivered the method itself (the no-skill version read the 3-day chart as a rolling "break of the lowest low of the previous three days", and misread "5 points" as 5%), and where arithmetic-heavy questions came out equally accurate with or without them
- **Repair log**: t21 exposed a near-neighbour ambiguity, after which the swing-chart card's description gained "produces chart signals only, makes no entry decision and no position sizing"; no other card needed rework
- **Stated honestly**: t22 ("analyse with the 3-day moving average") was judged as matching no capability — defensively reasonable, though the ideal behaviour is to trigger the swing-chart card and correct the convention (a moving average is not a swing chart); not scored as a failure, but recorded

## Repository layout

```text
gann-45-years-skill/
├── README.md                      ← Chinese version
├── README.en.md                   ← you are reading this
├── LICENSE                        ← MIT
├── BOOK_OVERVIEW.md               ← whole-book comprehension (Adler four-step, stage 0 output)
├── verified.md                    ← triple-verification conclusions for the 8 capability units
├── single/                        ← single-entry build
│   └── gann-45-years-skill/
│       ├── SKILL.md               ← entry: triggers + routing table + loading rules
│       ├── BUILD_MANIFEST.json    ← build manifest and file hashes
│       └── references/
│           ├── overview.md        ← whole-book overview
│           ├── capability-index.md  ← full intent and keyword index
│           ├── cheatsheet.md      ← decision-rule quick reference
│           ├── glossary.md        ← glossary
│           └── capabilities/      ← 8 capability cards
├── pack/                          ← multi-entry build (compact pack)
│   ├── BUILD_MANIFEST.json
│   ├── capability-destinations.json
│   ├── gann-45-years-skill-router/
│   │   ├── SKILL.md               ← source router entry
│   │   └── references/            ← 8 cards + indexes, called by the router
│   ├── gann-trade-risk-checklist-skill/
│   │   └── SKILL.md
│   ├── gann-percentage-levels-skill/
│   │   └── SKILL.md
│   ├── gann-trend-safe-entry-skill/
│   │   └── SKILL.md
│   ├── gann-time-cycle-calendar-skill/
│   │   └── SKILL.md
│   ├── gann-swing-charts-skill/
│   │   └── SKILL.md
│   └── gann-pyramid-profit-protect-skill/
│       └── SKILL.md
└── evals/                          ← trigger blind tests and output evaluation material
    ├── test-results.md             ← item-by-item scoring and repair log
    ├── output-cases.md             ← 16 output-evaluation scenarios and fixed assertions
    ├── trigger-suite.json          ← 32 trigger cases
    └── trigger-blind.json          ← blind-test execution record
```

## Usage

Clone the repository first:

```bash
git clone https://github.com/raphael-y7/gann-45-years-skill.git
```

### Install single (recommended first try)

```bash
# macOS / Linux
cp -r gann-45-years-skill/single/gann-45-years-skill ~/.agents/skills/
```

```powershell
# Windows
Copy-Item -Recurse .\gann-45-years-skill\single\gann-45-years-skill "$env:USERPROFILE\.agents\skills\"
```

### Install pack

Copy only the directories that contain a `SKILL.md`; do not copy the two JSON files under `pack/` into your skills directory:

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

> `~/.agents/skills` is the DSH skills directory; with another agent, use its own skills directory (for example `~/.claude/skills` for Claude Code).

### How to verify the install

Ask: "How many shares should I buy on this trade, and where does the stop go?" If the agent enters the 24-rule position calculation (risk budget ÷ per-share risk, asking back when no stop is given) instead of offering generic sizing advice, the install works. With the single build it reads the entry first and then routes to a card; with the pack build the matching capability is hit directly.

## Sources

- *45 Years in Wall Street* by William D. Gann
- Distilled from the whole book, producing 8 capability cards

## Notice

This repository publishes distilled skills, indexes and rule quick references only. It contains no PDF, EPUB, OCR files, screenshots or full-book transcripts of the source book. Quotations that appear in the capability cards serve solely to attribute methodology and keep the material auditable.

All numeric criteria in the book (3–5 point stops, the 5-point breakout tolerance, the 9-point swing threshold, adjustment-day windows, percentage levels, etc.) are case- and experience-based rules without statistical backtesting, and they all belong to the Dow point scale of the book's own era; re-scale them to the instrument's own volatility and declare the convention you use. Nothing in this repository is investment advice.

## License

[MIT](./LICENSE)

