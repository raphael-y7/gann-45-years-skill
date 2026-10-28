# verified.md — 通过三重验证的能力单元（阶段 1.5 产出）

> validation_version: task-first-v2
> 归并原则：候选（framework 40 + principle 79 + case 39 + counter-example 18 + glossary 26）先去重归并为能力单元，单元记录保留全部来源候选 ID。
> V2 均为 walkthrough（纸面演练），阶段 4 另做真实执行测试。
> 公共 Boundary 来源（适用所有单元）：p78 译者警示——绝对点位标尺（1点/日、3~5点止损、5点容差、9点阈值）基于 1949 年前道指/低价股时代，现代市场须按百分比/波动率重标定；全书"回验"为作者自选案例的事后解释，无样本外检验（BOOK_OVERVIEW 批判节）。

## U1 交易风控与资金管理自检系统

```yaml
id: U1
title: 交易风控与资金管理自检系统（24条永恒规则 + 资本10等分 + 止损/利润保护 + 期望管理）
type: framework+checklist+calculation
source_candidates: [f01, f02, f21, f22, f23, f24, f26, f27, f28, f29, f30, f31, f36, p01, p25, p26, p27, p28, p29, p31, p32, p34, p35, p36, p37, p74, p75, c35-c39(教训案例), ce01-ce14(边界素材)]
source_evidence:
  - location: 第2章 24条永恒的规则（L661-713）
  - location: 第2章 资本的安全/止损单/转变观念/过度交易/保护你的盈利/期待多少盈利/如何回应追加保证金/联名账户/买卖太早或太迟/危险的延误/人的因素（L715-787）
  - location: 第1章 输钱三主因（L505-515）
  - location: 第14章 大炒家教训与成功者共性（L4499-4519）
V1_source_sufficiency:
  passed: true
  reason: 24条规则清单完整带编号；每个执行条款（资本10等分、3~5点止损、3点利润上移、25%复利、追保清仓）在专节中独立讲透，输入输出数值口径齐全；失败模式（14条反例）与正反案例（第14章）配套。无未解决来源冲突。
V2_executability:
  passed: true
  check_mode: walkthrough
  input: 总资本10 000美元；拟以20美元买入某股，止损17美元（3点）
  expected: 单笔风险上限=10 000×10%=1 000美元；股数≤1 000÷3≈333股；浮盈3点后止损上移至成本20美元；预期利润≤3~5点时放弃交易；收到追保通知→清仓而非补钱
  observed: 全部条款可机械执行并给出唯一数值结论；24条清单可逐条勾选
V3_task_utility:
  passed: true
  expected_benefit: 事前防遗漏（单笔风险、止损、顺势、不摊平逐条过）；事后可定位违规条款；所有规则不依赖1949年点位绝对值（百分比口径），可跨市场直接落地——task-04 最高优先
decision: verified
```

## U2 百分比阻力位与中点计算程序

```yaml
id: U2
title: 百分比阻力位/支撑位与50%中点计算程序（含汇聚区判定）
type: calculation+procedure
source_candidates: [f06, p08, p40, p41, p42, p43, p64, p65, c06, c08, ce10, ce16]
source_evidence:
  - location: 第2章 规则3 按百分比买卖（L555-557）
  - location: 第4章 全章（L817-973：六级优先体系、三张示范表、中点算例、50%失守推定链、1929顶底全程回验）
  - location: 第9章 127~130/193~196/158~163 三处汇聚区算例（L4069-4160）
V1_source_sufficiency:
  passed: true
  reason: 计算公式、六级百分比优先级、起算点口径（极限高低价）、突破确认容差（5点）、汇聚区统计法均在正文完整给出并有至少一处从头到尾的算例（1929年顶 386.10 与底 195.35 的完整推演）；调整百分比系列（3~5%…85~87%）单处列全。
V2_executability:
  passed: true
  check_mode: walkthrough
  input: 极限最高价 H=386.10，极限最低价 L=40.56（书中数据）
  expected: 中点=(386.10+40.56)/2=213.33（书：213.33，1946年实顶213.36在其上0.03）；L+425%=40.56×5.25=212.94（书：212.94，双阻力汇聚）；H×50%=193.05（书：193.05，1929年11月底195.35在其上2.5点获支撑）
  observed: 三项独立复算与书中数值逐位一致；程序对任意新输入（用户自己市场的 H/L）可直接产出价位表
V3_task_utility:
  passed: true
  expected_benefit: 把"哪里是支撑/阻力"从主观判断变为可复算的价位表；统一口径（一律从极限高低价起算）；task-02 直达——作者自称"最伟大的发现"
decision: verified
```

## U3 趋势确认与最安全买卖点判定流程

```yaml
id: U3
title: 三层趋势确认与最安全买卖点判定（指数→股群→个股；顶底互换；次级调整后突破）
type: procedure+framework
source_candidates: [f03, f04, f05, f11, f13, f27, p02, p05, p06, p07, p16, p18, p20, p21, p22, p23, p30, p43, p63, c06, ce05, ce06, ce10, ce17]
source_evidence:
  - location: 第2章 规则1/2/9/10/11（L533-653，含双头双底容差、第四次必破、2日调整、次级底上破首轮顶）
  - location: 第7章 3日或更久的运动（L1592-1606，1942年三重底实例）
  - location: 第3章 配对案例中的趋势判定（L789-815）
V1_source_sufficiency:
  passed: true
  reason: 规则1/9/11 各自完整：趋势判据（HH/HL 对 LL/LH）、三层一致性流程、最安全买点四要素时序、最安全卖点对称结构、止损位（次级底下方1~3点）、5点有效突破容差，均有正文+实例。唯一缺口（f03：指数与个股矛盾时的裁决）由第3章案例补齐（按个股自身趋势操作），已在卡内注明。
V2_executability:
  passed: true
  check_mode: walkthrough
  input: 1942年4-6月道指摆动序列（书中数据：4月28日低92.69 → 5月11日高99.49 穿越4月21日顶98.02 → 3日下跌至96.39未破前低）
  expected: 三重底（92.69 距1938年低97.50与1935年低96均未破5点）=买入位；5月11日穿越3日顶=更高市场信号；此后至1946年5月29日未再破该低（书：正确）
  observed: 判定流程逐步可执行且与书中结果一致；对任意新摆动序列可产出多/空/区间结论+买卖点+止损位
V3_task_utility:
  passed: true
  expected_benefit: task-01+task-03 主干——回答"现在能不能买/卖、在哪买/卖、止损放哪"；强制等待确认信号，直接封堵 ce05/ce06（抄底摸顶、听消息）两类失败
decision: verified
```

## U4 时间周期变盘日历（方法+参数）

```yaml
id: U4
title: 时间周期变盘日历：调整时间层级 + 天数窗口 + 季节性日期 + 周年纪念日（含用自有数据重建日历的研究法）
type: framework+calculation
source_candidates: [f08, f09, f10, f12, f14, f15, p02, p09, p13, p14, p15, p17, p19, p45, p57, p58, p59, p60, p61, f16(部分), p62(部分), ce17]
source_evidence:
  - location: 第2章 规则4/8/10（L559-641：3周/6~7周/60~65天层级、九级天数窗口、全年两窗口日期表、节日表、年月周期）
  - location: 第5章 全章（1929-1949 逐段复盘的时间验证）
  - location: 第8章 月份统计（L3724-3937：35次顶部月份、36次熊市终点月份、69年极值统计、292次摆动时长分布）
  - location: 第9章 周年纪念日（L3977-4047）
  - location: 第6章 摆动记录研究法（L1271-1577）
V1_source_sufficiency:
  passed: true
  reason: 参数表（天数/月/年窗口、月度频率统计、锚点日期）全部成表给出；方法层（维护摆动记录→统计高频循环→尾声警惕）在 ch6/ch8 完整示范。已识别的书内参数不一致（glossary 备注：如时间窗口各章略有出入、p60 摆动档位与 p45 略有交叉）按"保留冲突+定位"处理，不阻塞方法本身——冲突点全部列入 Boundary，使用时以自有市场重建为准。
V2_executability:
  passed: true
  check_mode: walkthrough
  input: 极限低点 1949-6-14（书中当日）；另设自有市场低点 2024-2-5
  expected: 天数窗口=低点日期+{7~12,18~21,28~31,42~49,57~65,85~92,112~120,150~157,175~185}天；月周期={15,22,34,42,48,49}个月；周年纪念日=每年6月14日前后；2024-2-5 → 3月下旬(49天)、4月中(65天)、7月末(172~185天)等窗口
  observed: 日历生成完全机械化；月度统计表可直接转为"涨久防顶月/跌久防底月"优先级
V3_task_utility:
  passed: true
  expected_benefit: task-05+task-08——把"何时可能变盘"变成可提前生成的日历清单；"时间重于价格反转"（平衡过度判定）为趋势判断增加独立维度。风险已在 B 中前置：全部具体参数为 1949 年前道指归纳，无样本外检验，现代使用必须以自有数据重建（方法层 f14 完整可迁移）
decision: verified
```

## U5 3日图与9点摆动图维护及信号程序

```yaml
id: U5
title: 3日摆动图与9点摆动图：维护口径、信号读取与摆动幅度统计
type: procedure+calculation
source_candidates: [f17, f18, f19, f20, p49, p50, p51, p52, p53, p54, p55, p56, p24(速度标尺部分)]
source_evidence:
  - location: 第7章 维持3日图的规则 + 3日运动的例子（L1612-1640：六条维护口径+1940-1949全程实例）
  - location: 第7章 9点摆动图节 + 所有9点或更多的运动 + 30点运动的例子（L3074-3670）
  - location: 书末 13 张整页图（3日图A/B/C、9点摆动图1-4 等的读图口径，合并转写稿 L4685-4725）
  - location: 第2章 规则9 三层图表体系（L625）
V1_source_sufficiency:
  passed: true
  reason: 两图的维护规则逐条明确（何时记录/忽略、趋势线如何移动、例外条款），信号定义（破3日底/穿3日头、<9点反向=强势）清晰，464次9点运动与292次摆动统计给出分布数字，且 ch7 用 1940-1949 九年序列完整示范一遍。
V2_executability:
  passed: true
  check_mode: walkthrough
  input: 1941年4-6月道指日线（书中数据：4月23日/5月1日/16日/26日低点，5月26日为第二个更高的底）
  expected: 更高的底部序列成立→买入时点；止损=5月1日低点下方；穿越5月21日顶=趋势向上信号（书：正确，随后涨至7月22日131½）
  observed: 维护与信号规则可机械执行；对用户提供的新日线序列可产出摆动序列+信号（用户供数为前提条件，已列入 E）
V3_task_utility:
  passed: true
  expected_benefit: task-06+task-07——趋势过滤与噪声剔除的标准化工具；"反弹不足9点=弱势"等判据直接给出强弱结论；9点/30点/45点等点数阈值需按现代波动率重标定（B 前置）
decision: verified
```

## U6 成交量确认规则

```yaml
id: U6
title: 成交量确认：放量见顶、枯竭见底、牛市末年巨量
type: rule-set
source_candidates: [f35, p12, p66, p67, p68]
source_evidence:
  - location: 第2章 规则7 成交量（L577-579）
  - location: 第10章 全章（L4183-4260：1936-1949 月/年成交量总表与逐段判读）
V1_source_sufficiency:
  passed: true
  reason: 三条判据（老卖出位巨量=头部；长期下跌后地量=打底；牛市最后一年天量=终点）均有明确定义与多个带数据的实例（1938.10、1939.9、1946.1、1947.7、1948.5 见顶；1942.2-4 地量见底）。前提条款明确：必须与其他规则结合，单独不构成信号。
V2_executability:
  passed: true
  check_mode: walkthrough
  input: 1942年2-4月成交量约800万股/月且低于前数年同月（书中数据）
  expected: 长期下跌+地量=套现结束、打底信号（书：1942年4月28日为大牛市的起点）
  observed: 判据可机械套用（需相对化口径：与自身历史比较而非绝对股数——绝对值 800 万股为 1949 年尺度，已入 B）
V3_task_utility:
  passed: true
  expected_benefit: task-09——为价格/时间信号提供第三维确认；量价背离识别（价格新高+量不继=警惕）
decision: verified
```

## U7 加码与利润保护规程

```yaml
id: U7
title: 金字塔加码与利润保护跟随规程
type: procedure+calculation
source_candidates: [f24, f25, p28(联动), p33, p35(联动), c06]
source_evidence:
  - location: 第2章 何时加码（L755-761：突破法/调整法/时间加码、通用汽车全程例）
  - location: 第2章 保护你的盈利（L731-733）
  - location: 第2章 24规则 #20/#21（穿越阻力位再加、小盘加多大空大盘）
V1_source_sufficiency:
  passed: true
  reason: 两种加码法的触发条件、节奏（3/5/7/10/12点或首次调整时长）、约束（必带止损、仅活跃市场）完整；止损距离随利润放宽的算例明确（100点利润+20点历史调整→止损距20点）。f25 指出的"第几次调整后停止加码未明说"作为边界保留，不阻塞主体流程。
V2_executability:
  passed: true
  check_mode: walkthrough
  input: 某股首次重要调整=3周/7点（仿通用汽车指纹）；当前自顶部回调2周半至7点处、趋势向上
  expected: 按调整法此处为加码点；加码同时上移止损至保护初始资本位；浮盈3点的新仓止损=成本位
  observed: 加码/止损序列可逐步生成；熊市反向条款同样明确
V3_task_utility:
  passed: true
  expected_benefit: task-10——把"何时加仓、加多少、止损跟到哪"规则化；与 U1 联动封堵 ce08（错误时点加码）
decision: verified
```

## U8 多空配对交易流程（买强空弱）

```yaml
id: U8
title: 错流市多空配对：高位空弱势股 + 低位买强势股
type: procedure
source_candidates: [f33, p39, c06, f34(部分)]
source_evidence:
  - location: 第3章 买入一只股票而做空另一只 + 美国无线电和百事可乐（L789-815）
V1_source_sufficiency:
  passed: true
  reason: 单案例（1947年百事/无线电）给出完整闭环：选股判据（高点下移=弱、低位支撑=强）、双向止损、组合最大亏损预算（约400美元）、百分比目标管理（低价100%目标、50%回撤续持）、回补与反手条款。来源虽仅一例但机制在一处讲透（task-first 判据：一处完整说明可通过）；样本单薄入 B。
V2_executability:
  passed: true
  check_mode: walkthrough
  input: 弱势股自34½美元高点下移、现32美元；强势股8美元处多次获支撑
  expected: 空32止损35；买8止损7；组合风险≈(3+1)×100股=400美元+佣金；强势股15美元（+100%）了结；弱势股跌破20美元（自40½高点-50%）后继续持有空单并降止损至21
  observed: 全流程可复算，与书中操作一致
V3_task_utility:
  passed: true
  expected_benefit: 分化市况下的双向获利结构；预先锁定组合最大亏损——风控口径与 U1/U2 联动
decision: verified
```

---

## 汇总

| 单元 | 标题 | 覆盖任务 | 候选数 | decision |
|---|---|---|---|---|
| U1 | 交易风控与资金管理自检系统 | task-04 | 30+ | verified |
| U2 | 百分比阻力位与中点计算程序 | task-02 | 12 | verified |
| U3 | 趋势确认与最安全买卖点判定 | task-01/03 | 24 | verified |
| U4 | 时间周期变盘日历 | task-05/08 | 21 | verified |
| U5 | 3日图/9点摆动图程序 | task-06/07 | 13 | verified |
| U6 | 成交量确认规则 | task-09 | 5 | verified |
| U7 | 加码与利润保护规程 | task-10 | 6 | verified |
| U8 | 多空配对交易流程 | task-11(半) | 4 | verified |

- 去重归并记录：f06≡p40（U2 保留双 ID）；f08≡p09、f09≡p13/p17（U4）；f21≡p25、f22≡p26、f23≡p27/p29（U1）；f17≡p49/p50、f18≡p51（U5）；f24≡p28（U7）；f33≡p39（U8）；f02≡p02（并入 U3 支撑原则+references）。
- 用户轻确认：用户按"减少中途空闲"指示授权连续执行；四类分流（8 verified / reference 清单见 references.md / 1 needs_review / 0 rejected）与重要缺口（task-11 量化标准、task-12 时代性）将在最终交付时一并呈报复核。
