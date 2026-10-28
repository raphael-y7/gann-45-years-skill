# candidates/counter-example.md — 反例提取（失败模式清单）

> 阶段 1 产出之一。因并发限制，反例提取器三次启动失败，按 skill 降级方案由主对话串行执行，格式与 extractor 规程一致。
> 素材来源：第1章（L475-521）、第2章 24条规则禁令与执行条款（L665-787）、第12章（L4372-4404）、第14章（L4499-4519）。

```yaml
- id: ce01
  title: 过度交易（所有失败模式之首）
  type: counter-example
  source_chapter: 第1章 为什么你会在股市里输钱；第2章 24条永恒的规则#3；第14章
  source_quote: |
    "对于他们的资本，他们交易过度或买卖过于频繁。"
    "这是所有投机炒家最大的错误——过度交易，将谨慎忘得一干二净，而没有考虑意外会出现。"
  failure_mode: 相对资本下过重的仓位、买卖过于频繁，一次反向波动或连错几次即重创本金。
  mechanism: 仓位过重放大波动对心态的反噬，迫使交易者在最不利时刻平仓；频繁交易累积佣金与情绪损耗，且每次决策质量下降。
  warning_signs:
    - 单笔风险超过资本的1/10
    - 一天之内多次进出同一标的
    - "因为闲不住"而下单
  bound_to: [资本十等分风控, 交易前自检清单]
  tags: [counter-example, risk-control, overtrading]

- id: ce02
  title: 不设止损单 / 设置后撤销
  type: counter-example
  source_chapter: 第2章 24条规则#2/#16、止损单、转变观念
  source_quote: |
    "止损单让你错误地离场一次，它会在下面九次中让你正确地脱身来弥补。"
    "撤消你的止损单——一旦设置了之后，并非基于良好的判断，而是基于希望。"
  failure_mode: 交易时不设止损，或亏损后撤销止损"扛单"，小亏拖成大亏直至爆仓。
  mechanism: 希望替代事实；十次中一次被扫损的负面记忆被放大，导致放弃那九次的保护；撤销止损后失去强制纠错机制。
  warning_signs:
    - "再等等，它总会回来的"
    - 入场时"还没想好止损放哪"
    - 曾有止损被扫后行情反转的经历并因此弃用
  bound_to: [止损纪律, 趋势确认后入场]
  tags: [counter-example, stop-loss, discipline]

- id: ce03
  title: 均分损失（摊平成本）
  type: counter-example
  source_chapter: 第2章 24条永恒的规则#13
  source_quote: |
    "永不满仓损失。这是交易者会犯下的最糟糕的错误之一。"（译文作"永不均分损失"）
  failure_mode: 越跌越买以"摊低成本"，在下跌趋势中不断加码多头，最终满仓套牢。
  mechanism: 摊平只适用于计划内的分批建仓，被用作战损补救时等于给亏损头寸加码——逆势加码的特例，趋势未反转前损失呈线性放大。
  warning_signs:
    - "跌了这么多，再买点把成本摊下来"
    - 补仓理由只有"更便宜了"，没有趋势反转证据
  bound_to: [加码规则, 趋势确认后入场]
  tags: [counter-example, averaging-down, position-management]

- id: ce04
  title: 凭希望与恐惧交易（人性最大弱点）
  type: counter-example
  source_chapter: 第2章 人的因素——最大的弱点；第14章
  source_quote: |
    "你凭希望或恐惧，而不是事实行事。你会延误。你会急躁。"
    "但是人类最大的敌人——希望，使他一直持仓至灾难降临。"
  failure_mode: 亏损时靠希望持仓不动，盈利时靠恐惧急忙兑现；卖出常在最低附近、买入常在最高附近。
  mechanism: 情绪与事实置换：持仓后自动过滤利空信息（见 ce05），亏损扩大触发否认；解药是规则化、机械化执行。
  warning_signs:
    - 只找支持自己仓位的信息
    - 盈利单拿不住、亏损单拿得稳
    - 把损失归咎于市场/庄家/消息
  bound_to: [交易前自检清单, 止损纪律]
  tags: [counter-example, psychology, hope-fear]

- id: ce05
  title: 听小道消息/他人荐股入市
  type: counter-example
  source_chapter: 第1章 为什么你会在股市里输钱；第2章 交易者不愿知道什么
  source_quote: |
    "他们根据小道消息，或他人的想法购买股票，而他们自己没有这个股票会上涨的任何具体知识。"
  failure_mode: 依据无根据的推荐建仓，不知道依据就无信心持有，涨跌都被情绪支配，错了也不知道错在哪。
  mechanism: 无独立判断→无法评估仓位对错→出入市时机全随机；"90%以上的失败源于没有止损单和过度交易"，两者都源于无知入市。
  warning_signs:
    - 说不出这笔交易依据哪条规则
    - 靠股评、群消息、亲友内幕决策
  bound_to: [趋势确认后入场, 交易前自检清单]
  tags: [counter-example, information-hygiene]

- id: ce06
  title: 逆势而为
  type: counter-example
  source_chapter: 第2章 24条永恒的规则#5、规则11
  source_quote: |
    "永远顺势而为，不要逆势而行。在强势中买股，在弱势中卖股。"
    "如果你根据走势图无法确定趋势，就永不买卖。"
  failure_mode: 在下跌趋势中抄底、上涨趋势中摸顶；趋势不明时强行交易。
  mechanism: 趋势是概率优势的来源，逆势等于把优势让给对手；时间循环未走完时任何消息都扭转不了趋势（第1章保证金实例）。
  warning_signs:
    - "跌了这么多该到底了"
    - 信号只有价格便宜/贵，无趋势结构证据
  bound_to: [趋势确认后入场, 时间周期监测]
  tags: [counter-example, trend-following]

- id: ce07
  title: 拿不准仍持仓 + 出入市过于频繁
  type: counter-example
  source_chapter: 第2章 24条永恒的规则#6/#17
  source_quote: |
    "拿不准的时候就退出，而且不要在拿不准的时候入市。"
    "避免出入市过于频繁。"
  failure_mode: 信号模糊时不愿离场（怕踏空），又忍不住反复试探性建仓。
  mechanism: 拿不准=无优势下注；频繁试探累积成本并制造情绪波动，破坏后续决策质量。
  warning_signs:
    - 一周内对同一标的多空反复
    - 仓位理由从"规则信号"变成"感觉"
  bound_to: [趋势确认后入场, 交易前自检清单]
  tags: [counter-example, indecision, churn]

- id: ce08
  title: 在错误的时候加码
  type: counter-example
  source_chapter: 第2章 24条永恒的规则#20、何时加码
  source_quote: |
    "等股票非常活跃并穿越了阻力位之后再加码买入，而且等股票跌破派发区域后再加码卖出。"
  failure_mode: 亏损时加码摊平（同 ce03）或在突破发生前抢跑加码，把平均成本置于危险区。
  mechanism: 正确加码的前提是"突破确认+按调整幅度节奏"；抢跑加码使全部仓位暴露于假突破，止损位被迫下移。
  warning_signs:
    - 加码时股价尚未穿越阻力位
    - 加码后止损位比原计划更深
  bound_to: [加码规则, 百分比阻力位计算]
  tags: [counter-example, pyramiding]

- id: ce09
  title: 用对冲代替认赔
  type: counter-example
  source_chapter: 第2章 24条永恒的规则#22
  source_quote: |
    "永不对冲。如果你做多一只股票，而它开始下跌，就不要放空另一只股票来对冲它。你该离场；认赔并等待另一个机会。"
  failure_mode: 持仓亏损后放空另一只"同板块股票"对冲，两头挨打，两头付佣金。
  mechanism: 两只个股节奏不同步，对冲无法封闭风险，只是拖延认错；正确动作是直接了结错误头寸。
  warning_signs:
    - "我做空一点XX来对冲我的YY"
    - 对冲仓与原仓分属不同个股而非同一工具
  bound_to: [止损纪律, 选股与独立行情]
  tags: [counter-example, hedging]

- id: ce10
  title: 因价格低而买、因价格高而空
  type: counter-example
  source_chapter: 第2章 24条永恒的规则#19
  source_quote: |
    "永不仅因为股价低而买入，或因为股价高而放空。"
  failure_mode: 把绝对价格当估值锚：低价股=便宜、高价股=贵，无视趋势与百分比位置。
  mechanism: 价格高低不构成买卖依据，只有趋势信号+阻力位确认才是；低价股可能退市，高价股可能翻倍（对照 ch3 无线电 2.5→500美元案例）。
  warning_signs:
    - "这股才3块钱，跌无可跌"
    - 空头理由只有"涨太多了"
  bound_to: [趋势确认后入场, 百分比阻力位计算]
  tags: [counter-example, price-anchoring]

- id: ce11
  title: 收到追保通知后继续死捂
  type: counter-example
  source_chapter: 第2章 如何回应追加保证金的通知
  source_quote: |
    "如果经纪人不得不通知你追加保证金，那么一定是有什么不对头的地方，因此最好是清仓离场。"
  failure_mode: 收到追保通知后不断补钱，直到第二次、第三次追保，在一笔交易上输光全部资本。
  mechanism: 追保通知本身证明仓位与判断已错；补钱是把新资金投入已被证伪的头寸——十有八九连续追加直至毁灭。
  warning_signs:
    - 收到追保通知的第一反应是转账而不是减仓
    - "市场一回来我就出"
  bound_to: [资本十等分风控, 止损纪律]
  tags: [counter-example, margin-call]

- id: ce12
  title: 联名账户/合伙交易
  type: counter-example
  source_chapter: 第2章 联名账户
  source_quote: |
    "一个头脑要在股市中操作并保持正确很难，两个头脑要在股市中保持一致并发挥作用则是难上加难。"
  failure_mode: 两人共管账户，入场容易达成一致、退出永远谈不拢，盈利单拖成亏损单。
  mechanism: 出场决策需要对时机的独断；合伙制在获利了结上制造僵局，责任分散让双方都等待对方行动。
  warning_signs:
    - 开仓前没约定"谁拍板离场"
    - 已经出现"你想出我想留"的争执
  bound_to: [交易前自检清单]
  tags: [counter-example, account-structure]

- id: ce13
  title: 延误行动（该出手时不动手）
  type: counter-example
  source_chapter: 第2章 危险的延误
  source_quote: |
    "延误总是危险的。现在立即采取行动，比期待不确定的时间要好得多。你永远不应在疲劳或沮丧的时候交易。"
  failure_mode: 看对了行情却不行动，或等"更好的价位"，等来的是趋势走完或反转；在疲劳/情绪差时勉强交易。
  mechanism: 拖延期间判断持续贬值；身体与情绪状态差时判断力系统性下降——健康是交易资本的一部分。
  warning_signs:
    - 信号已触发却"再确认一下"超过一个交易日
    - 熬夜、生病、大额生活压力期间仍在交易
  bound_to: [趋势确认后入场, 止损纪律]
  tags: [counter-example, procrastination]

- id: ce14
  title: 长期连胜后放大交易规模
  type: counter-example
  source_chapter: 第2章 24条永恒的规则#24
  source_quote: |
    "避免在长期的成功或赢利后增加交易。"
  failure_mode: 连赢后自信膨胀，加大单笔仓位与频率，一次回吐全部利润。
  mechanism: 连胜常来自市场风格与规则暂时匹配，而非技能永久提升；规模放大后同样的规则容错空间被压缩（对照 ch14 大炒家"赚几百万后采用另一种判断"）。
  warning_signs:
    - 连续盈利后想"上杠杆/上仓位"
    - 开始觉得"这次不一样"
  bound_to: [资本十等分风控, 期望管理]
  tags: [counter-example, overconfidence-after-winning]

- id: ce15
  title: 试图操纵市场/垄断（权力欲陷阱）
  type: counter-example
  source_chapter: 第14章 从前的大炒家
  source_quote: |
    "他们只渴望金钱能够带来的力量，而且要垄断市场。结果几乎所有试图这样做的人都落得了同样的下场。他们破产了。"
  failure_mode: 资金做大后试图逼仓垄断（莱特囤小麦、萨利/普莱斯/斯凯勒斯囤棉花、克劳福买断食品），被交割狙击或崩盘反噬。
  mechanism: 垄断把价格推离供求均衡，吸引交割供给与对手盘；"意外总会出现"，无人聪明到能垄断市场（阿默运小麦破莱特垄断）。
  warning_signs:
    - 持仓量大到影响价格本身
    - 相信"我买不完它就不会跌"
  bound_to: [期望管理, 资本十等分风控]
  tags: [counter-example, cornering, power-urge, reported-case]

- id: ce16
  title: 不研究历史记录（无知于"离谱价位"）
  type: counter-example
  source_chapter: 第14章 乔丹棉花崩盘
  source_quote: |
    "如果他仔细研究过以往战时的价格…… cotton 43美分……1923年 37½美分……他本可以知道市场已处于不正常的水平。"
  failure_mode: 不查历史极值记录，在历史区间的极端位置继续追买/追卖（乔丹1946年棉花3928点追多，一个月跌至2310）。
  mechanism: 历史极值记录标出"不正常水平"；越接近历史极值，均值回归与对手反转的力量越强，跟风盘成为唯一买盘。
  warning_signs:
    - 价格处于历史区间前1%位置仍在顺势加码
    - 说不出这个标的上一次极值是多少
  bound_to: [百分比阻力位计算, 时间周期监测]
  tags: [counter-example, history-blindness, reported-case]

- id: ce17
  title: 误信政策/利多能扭转趋势
  type: counter-example
  source_chapter: 第1章 成交量减少；第14章
  source_quote: |
    "只要时间循环显示下降趋势，那么什么都不能阻挡市场的下跌。"
    "连美国政府都不能阻止棉花市场的下跌。"
  failure_mode: 把政策救市、重大利多当作逆势入场的理由（1949年降保证金看涨实例；乔丹崩盘中政府被迫救场）。
  mechanism: 消息本身不改变趋势，趋势由时间循环与供求决定；利好出尽在下跌趋势中反而成为出货窗口。
  warning_signs:
    - 因"国家队/利好政策"逆势抄底
    - 交易理由是新闻而非规则信号
  bound_to: [趋势确认后入场, 成交量确认]
  tags: [counter-example, news-trading]

- id: ce18
  title: 忽视期权/权证的卖方风险与归零风险
  type: counter-example
  source_chapter: 第12章 看涨期权、看跌期权、认股权和权证
  source_quote: |
    "期权买方可能损失的最大金额是期权价格，而期权卖方则要承受巨大的亏损风险。"（译者注）
    "当你买进任何一只股票的权证时，你能够损失的全部是你为这种权证支付的价格。"
  failure_mode: 把"低风险"误读为"无风险"：卖方裸卖期权承受巨大尾部风险；买方满仓权证归零风险常在（权证可跌至几美分）。
  mechanism: 期权/权证的有限损失仅指买方权利金口径；卖方风险无限，且权证时间价值衰减使"便宜"更便宜——低价不构成买入理由（同 ce10）。
  warning_signs:
    - 为权利金收入裸卖期权
    - 用大仓位买深度虚值/临期权证
  bound_to: [期权权证参考, 资本十等分风控]
  tags: [counter-example, options, tail-risk]
```

## 提取器自检

- [x] 每条都有 failure_mode 和 mechanism（不止"这是错的"）
- [x] warning_signs 可操作（B 段信号来源）
- [x] bound_to 指向受限制的正面能力（风控清单/趋势确认/加码规则/百分比计算等）
- [x] 原文引用 ≤150 字/段，位置可定位
- [x] ce15/ce16 标注 reported_case（第14章转述）；ce01-ce14 均为作者直接警告
