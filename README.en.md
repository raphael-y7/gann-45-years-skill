<h1 align="center">Gann 45 Years Skill</h1>

<p align="center"><a href="README.md">中文</a> | English</p>

An AI skill pack for immediate use — it distills the reproducible rule system built on "time, price and volume" from William D. Gann's *45 Years in Wall Street* into 8 capability cards that can be triggered individually or combined.

It is not a book summary, nor a reading response — it breaks the reusable methodology in the book into skill modules that can be triggered, executed and tested.

## What these skills solve

- You cannot work out how many shares to buy before entering: capital split into 10 parts, single-trade risk capped at 10%, shares = risk budget ÷ per-share risk; when the stop price cannot be stated, the pack refuses to size the position instead of guessing
- You only know "this looks like support" but cannot name the price: the cards build a price table from the historic extreme high and extreme low by fixed percentages, always compute the 50% midpoint, and count how many sources cluster in the same narrow band
- You cannot tell "higher high + higher low" apart from "it bounced because it fell a lot": three-layer consistency and the four elements of the safest entry are checked one by one, and a missing element yields "structure incomplete, wait"
- The time dimension is pure intuition: the adjustment-time hierarchy and day windows can be turned into a turning-point calendar ahead of time, and "this adjustment lasted longer than the previous one for the first time" has an explicit criterion
- How the 3-day chart and the 9-point swing chart are actually maintained, and what counts as a signal: the maintenance convention (any counter-move of 2 days or fewer is ignored) plus the definitions of "breaking the 3-day bottom" and "crossing the 3-day top"
- Whether to pyramid after a profit, where the trailing stop goes, and whether to "average down" a loser or "short something else to hedge": the pyramid fingerprint and the stop sequence can be generated, while averaging down and hedging are red lines the book explicitly forbids

## What was distilled

8 capability cards, grouped in the order "hold the floor first, locate second, advance last" (slugs match the `capabilities` entries in `bundle/verified.yaml` one for one):

- **Risk discipline**: `gann-trade-risk-checklist-skill` (trade risk and money-management self-check, the 24 timeless rules)
- **Price and trend**: `gann-percentage-levels-skill` (percentage resistance levels and the 50% midpoint), `gann-trend-safe-entry-skill` (trend confirmation and the safest entry/exit)
- **Time and charts**: `gann-time-cycle-calendar-skill` (time-cycle turning-point calendar), `gann-swing-charts-skill` (3-day chart and 9-point swing chart maintenance and signals)
- **Volume**: `gann-volume-confirm-skill` (volume confirmation: climax tops and exhaustion bottoms)
- **Advanced operations**: `gann-pyramid-profit-protect-skill` (pyramiding and profit protection), `gann-pair-trade-skill` (cross-current long/short pairing, long the strong and short the weak)

## Two packaging modes: single and pack

The same 8 capability cards are compiled twice, at two granularities. The content is identical; the only difference is how many entries an agent can discover.

| | single (one entry) | pack (compact pack, multiple entries) |
|---|---|---|
| Discoverable entries | **1**: `gann-45-years-skill` | **7**: one source router + 6 promoted standalone skills |
| Where the 8 cards live | All inside the entry's `references/capabilities/`, loaded 1–2 at a time by the routing table | 6 high-frequency cards become standalone skills; volume confirmation and pair trading stay in the router's `references/` |
| Triggering | Only the entry description participates in matching; routing happens after entry | The 6 high-frequency capabilities are matched directly, one hop fewer |
| Upgrades | Replace 1 directory | Replace 7 directories |

The 6 cards promoted to standalone skills in the pack:

- `gann-trade-risk-checklist-skill` — trade risk and money-management self-check (the 24 timeless rules)
- `gann-percentage-levels-skill` — percentage resistance levels and the 50% midpoint
- `gann-trend-safe-entry-skill` — trend confirmation and the safest entry/exit
- `gann-time-cycle-calendar-skill` — time-cycle turning-point calendar
- `gann-swing-charts-skill` — 3-day chart and 9-point swing chart maintenance and signals
- `gann-pyramid-profit-protect-skill` — pyramiding and profit protection

### Which one to install

Pick by the way you work, and **install only one**:

| How you work | Recommended | Why |
|---|---|---|
| You use DSH / Codex / Claude Code with a skills directory and want a clean list | single | Takes 1 slot, loses none of the 8 cards |
| Your daily questions concentrate on "how much to buy / where is support / can I buy now / when does it turn / what does the 3-day chart say / where does the trailing stop go" | pack | Those are exactly the promoted standalone skills, matched directly |
| You distribute to several agents or teammates who pick what they need | pack | They can install only the standalone skills they want |
| You want to install once and maintain one directory | single | Upgrades replace a single directory |

> Both builds come from the same bundle and carry identical capabilities. **Installing both will double-trigger**, so pick one.

## Examples

### Example 1: historic high 120, low 24, price 78 — where can I buy the pullback?

**User question**

"This stock's historic high is 120, its low is 24, and it trades at 78 now. Where can I buy the pullback? How much room is above?"

**How the skill reasons**

- Enter `gann-percentage-levels-skill`: pin the starting points first — they must be the extreme high H=120 and the extreme low L=24; if the user offered arbitrary pivots, ask for confirmation instead of computing (the card's B section lists "starting-point discipline" as the most common misuse)
- Build the price table: midpoint (120+24)/2 = 72.00; from L upward +50% = 36.00, +100% = 48.00, +200% = 72.00, +300% = 96.00; from H downward −25% = 90.00, −50% = 60.00, −75% = 30.00
- Cluster statistics: 72.00 comes from both "midpoint" and "L+200%", so the number of sources must be reported separately (the book's criterion is ≥3 sources for a confluence zone; with 2 sources here, say so honestly)
- Breakout test: the card requires price to exceed the tolerance beyond a resistance level to count as valid (5 points in the book, where 1 point = 1 dollar in the old convention); modern use must first rescale by the instrument's own volatility percentage and state which number was used; anything inside the tolerance is unconfirmed
- Boundary: this card only answers "where are the walls" and gives no buy/sell signal — direction goes to `gann-trend-safe-entry-skill`, position size to `gann-trade-risk-checklist-skill`

**Sample answer**

> Pin the starting points first: are 120 and 24 really this stock's historic extreme high and low? If not, the whole table has to be rebuilt — that is the easiest way to misuse this card. With these two numbers: the midpoint is 72.00, and it is also the L+200% level — two sources land on the same price, which carries the highest weight of any single level in the book. Below that are H−50% = 60.00 and L+100% = 48.00; above are H−25% = 90.00 and L+300% = 96.00. At 78 the price sits above the midpoint and below 90, so it is "still inside the resistance zone", not a valid breakout. So on "where can I buy the pullback", this card can only answer "72 is the first level worth watching", not "buy at 72": a break below 72 that fails to recover must be marked extremely weak, and the next reference level has to be stated together with the convention used. For an actual buy/sell conclusion, go to the trend card and check "higher high + higher low" and the four elements of the safest entry; for how many shares, go to the risk card.

### Example 2: down 20% — should I average down?

**User question**

"I bought at 30, it is at 24 now, a 20% paper loss. Should I add another lot to lower my average cost?"

**How the skill reasons**

- Enter `gann-pyramid-profit-protect-skill`: step 5 of its execution procedure is a failure branch — on detecting an "add to a loser" intent it stops immediately and outputs the prohibition (never average a loss), offering no pyramiding plan; its B section also states the card only adds in the direction of profit, the exact opposite of grid / martingale-style adding into losses
- Switch to `gann-trade-risk-checklist-skill`: "never average a loss (no averaging down)" and "never hedge" are explicit clauses in its prohibition layer; violating either yields "do not trade" plus the clause names
- Position convention: single-trade risk = total capital × 10%; per-share risk = |current price − stop price|; share cap = risk ÷ per-share risk. The user gave no stop price, so the first step is not adding — it is setting the stop

**Sample answer**

> No. In the book this is "never average a loss" — not "not advisable", but a prohibition; the pyramiding card stops as soon as it detects adding to a loser and gives no plan. To go through the numbers, use the risk card: single-trade risk is capped at 10% of total capital, per-share risk is the current price minus the stop price, and the share cap is risk divided by per-share risk — you have not even set a stop, so the first step is to write the stop down, not to add. Adding does lower the average cost, but it also enlarges the position and the maximum loss, which overthrows the "capital in 10 parts, never more than 10% per trade" red line. The book's handling of this situation: attribute the loss to yourself first, go back through the 24 rules to locate which one you broke and record it, then exit and do not repeat it. One more note: the pyramiding card only covers "adding to an existing profitable position and trailing the stop", never adding into a loss — the exact opposite of grid / martingale adding, so do not mix the two systems.

## How these skills were generated

These skills were produced with the **[cangjie-skill](https://github.com/kangarooking/cangjie-skill)** RIA-TV++ pipeline, in six stages:

1. **Whole-book comprehension (Adler analysis)** — apply Mortimer Adler's analytical reading method to the book: structure, interpretation, criticism, application, deciding up front which layer is usable and which can only serve as case material
2. **Parallel extraction** — several specialized extractors (frameworks, principles, cases, counter-examples, terminology) mine candidate methodology units from the source text
3. **Triple verification** — every candidate must pass three checks: at least two independent in-book supports (cross-domain), the ability to answer questions the book never explicitly addresses (predictive power), and not being common sense (distinctiveness)
4. **RIA++ construction** — structure each unit along R (quotation) / I (restatement in own words) / A1 (in-book case) / A2 (future trigger scenario) / E (executable steps) / B (boundaries and blind spots)
5. **Zettelkasten linking** — map dependencies, contrasts and combinations between cards, producing the capability index and routing table
6. **Trigger and output testing** — write trigger blind tests (including decoy questions: fire when they should, stay silent when they should not) and output evaluation scenarios for every card; failing cards go back for rework and are re-verified afterwards

This book adds one more layer of selection: what lasts is the "risk-discipline layer" (the 24 timeless rules, capital in 10 parts, the stop-loss system), while the "historical narrative layer" (the rise and fall of big operators, war cycles, forecasts about the future) is kept only as case and background and is never compiled into an executable capability. The price, time and chart layers are portable, but their absolute point parameters belong to the Dow scale of the book's era, so every card writes "must be rescaled to the instrument's own volatility and the convention declared" into its boundary section.

## Testing and verification

This repository publishes the evaluation material from the audit directory alongside the skills: `evals/test-prompts/` holds the per-entry trigger cases, `evals/trigger-suite.json` and `evals/trigger-blind.json` are the trigger test set and the blind-run record, `evals/output-cases.md` holds the output-evaluation scenarios and fixed assertions, and `evals/test-results.md` is the item-by-item scoring and rework log — including what did not work, not just the passes. The test host was ZCode / GLM-5.3, and the blind runs were executed by an independent sub-agent that took no part in the distillation and could not see the expected answers or assertions.

- **Trigger blind tests**: 32 prompts × 8 capabilities — 30 / 32 hit exactly, 2 borderline-but-acceptable (t21, t22), **0 false activations**; all 8 cross-capability decoys were correctly avoided
- **Output evaluation**: 8 capabilities × normal / boundary = 16 scenarios, **16 / 16 passed, 0 failures**
- **With-card vs without-card control**: all 16 scenarios were run both ways, and the report summarizes 5 key differences — where the cards delivered the method itself (the no-card run misread the 3-day chart as a rolling "below the prior three-day low" convention and misread "5 points" as 5%), and where calculation questions matched the baseline arithmetic
- **Rework record**: after t21 exposed a neighbouring-capability ambiguity, the swing-chart card's description gained "only produces chart signals, makes no entry decision and no position sizing"; no other card went back for rework
- **Stated honestly**: t22 ("analyze with a 3-day moving average") was judged as having no matching capability — defensively reasonable, though the ideal behaviour is to trigger the swing-chart card and correct the convention (a moving average is not a swing chart); not counted as a failure but recorded

## Repository layout

```text
gann-45-years-skill/
├── README.md                      ← Chinese version
├── README.en.md                   ← you are reading this
├── LICENSE                        ← MIT
├── BOOK_OVERVIEW.md               ← whole-book comprehension (Adler four-step, stage 0 output)
├── verified.md                    ← triple-verification conclusions for the 8 capability units
├── INDEX.md                       ← skill map: capability table + dependencies + loading order
├── TEST_SUMMARY.md                ← stage 4 stress-test summary (scope / structure checks / results)
├── CANGJIE_ADAPTATION.md          ← Cangjie adaptation notes (text state / goals / evidence rules / boundaries)
├── candidates/                    ← stage 1 extracted candidate pool (202 raw candidates, uncompiled)
│   ├── framework.md               ← 40 framework candidates
│   ├── principle.md               ← 79 principle candidates
│   ├── case.md                    ← 39 case candidates
│   ├── counter-example.md         ← 18 counter-example candidates
│   └── glossary.md                ← 26 glossary candidates
├── bundle/                        ← compile source of truth (the pre-compile layer)
│   ├── verified.yaml              ← canonical definitions (slug / importance / destination / evidence)
│   ├── cards/                     ← 8 capability cards (R / I / A1 / A2 / E / B)
│   └── book/
│       ├── overview.md            ← whole-book overview
│       └── glossary.md            ← glossary
├── single/                        ← single-entry build
│   └── gann-45-years-skill/
│       ├── SKILL.md               ← entry: triggers + routing table + loading rules
│       ├── BUILD_MANIFEST.json    ← build manifest and file hashes
│       ├── test-prompts.json      ← entry-level trigger and boundary cases (10)
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
│   │   ├── test-prompts.json      ← router entry cases (7)
│   │   └── references/            ← 8 cards + indexes, called by the router
│   ├── gann-trade-risk-checklist-skill/
│   │   ├── SKILL.md
│   │   └── test-prompts.json      ← trigger and boundary cases (9)
│   ├── gann-percentage-levels-skill/
│   │   ├── SKILL.md
│   │   └── test-prompts.json      ← trigger and boundary cases (8)
│   ├── gann-trend-safe-entry-skill/
│   │   ├── SKILL.md
│   │   └── test-prompts.json      ← trigger and boundary cases (9)
│   ├── gann-time-cycle-calendar-skill/
│   │   ├── SKILL.md
│   │   └── test-prompts.json      ← trigger and boundary cases (9)
│   ├── gann-swing-charts-skill/
│   │   ├── SKILL.md
│   │   └── test-prompts.json      ← trigger and boundary cases (8)
│   └── gann-pyramid-profit-protect-skill/
│       ├── SKILL.md
│       └── test-prompts.json      ← trigger and boundary cases (8)
└── evals/                          ← trigger blind tests and output evaluation material
    ├── test-results.md             ← item-by-item scoring and rework log
    ├── output-cases.md             ← 16 output-evaluation scenarios and fixed assertions
    ├── trigger-suite.json          ← 32 trigger cases
    ├── trigger-blind.json          ← blind-run record
    └── test-prompts/               ← 9 per-entry case files (copies of the test-prompts.json in each skill directory)
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

Ask: "How many shares should I buy for this trade, and where does the stop go?" If the agent enters the 24-rule position calculation (risk budget ÷ per-share risk, asking back when no stop is given) instead of giving generic sizing advice, the install works. With the single build it reads the entry first and then routes to a card; with the pack build the matching capability is hit directly.

## Sources

- *45 Years in Wall Street* by William D. Gann

## Notice

This repository publishes distilled skills, indexes and rule quick references only. It contains no PDF, EPUB, OCR files, screenshots or full-book transcripts of the source book. Quotations that appear in the capability cards serve solely to attribute methodology and keep the material auditable.

All numeric criteria in the book (3–5 point stops, the 5-point breakout tolerance, the 9-point swing threshold, adjustment day windows, percentage tiers, etc.) are case- and experience-based rules without statistical backtesting, and they all belong to the Dow point scale of the book's era; test them on your own instruments, rescale them to each instrument's volatility and declare the convention you use. Nothing in this repository is investment advice.

## License

[MIT](./LICENSE)
