# coverage-audit.md — 原书关键任务覆盖审计（阶段 1.5 产出）

> 基准：BOOK_OVERVIEW.md 原书关键任务清单（task-01~12），不从旧 verified 反推。

| task_id | 读者任务 | 原文位置 | 对应候选 | decision | 最终去向 |
|---|---|---|---|---|---|
| task-01 | 判定市场大趋势方向 | 第2章规则1/9/10 | f03/f04/p05/p16/p18 | verified | U3 |
| task-02 | 计算百分比阻力位/支撑位表 | 第4章 | f06/p40/p41/p64 | verified | U2 |
| task-03 | 确定最安全买卖点 | 第2章规则2/11 | f05/p20/p21/p43 | verified | U3 |
| task-04 | 交易前风控自检 | 第2章24规则+资本安全 | f21-f24/p25-p29 | verified | U1 |
| task-05 | 判断调整/反弹时间窗口 | 第2章规则4/8、第5章 | f08/p09/p14/p45 | verified | U4 |
| task-06 | 维护3日图 | 第7章 | f17/p49/p50 | verified | U5 |
| task-07 | 维护9点摆动图 | 第7章后半 | f18/p51-p53 | verified | U5 |
| task-08 | 标记季节日期与周年纪念日 | 第2章规则8/10、第9章 | f09/f15/p13/p17/p61 | verified | U4 |
| task-09 | 成交量确认趋势变化 | 第10章 | f35/p66-p68 | verified | U6 |
| task-10 | 加码与利润保护计划 | 第2章何时加码/保护盈利 | f25/p33/p28 | verified | U7 |
| task-11 | 挑选独立行情个股 | 第3章 | f32（识别）/f33/p39（配对） | 识别=needs_review（量化标准缺失）；配对=verified | 配对→U8；识别→needs-review.md 缺口如实登记 |
| task-12 | 期权/权证低风险用法 | 第12章 | f36/p70-p72 | reference（时代性） | references.md→overview 参考节 |

## 覆盖结论

- 12 项关键任务全部有候选及明确去向：8 项 verified、1 项 verified（task-11 的配对半区）、1 项 needs_review（task-11 的识别半区，缺口如实登记）、1 项 reference（task-12）、task-06/07 合并于 U5。
- 未发现"重要任务无候选"的遗漏；二手来源（导读/译者序/附录B）均已标注且只进 reference 层。
- 附加覆盖（超出任务清单但用户目的相关）：失败模式 18 条（→各卡 B 段）、案例 39 条（→各卡 A1 段）、术语 26 条（→GLOSSARY）。
