# Stage 4 压力测试摘要

> 数据来源：归档目录 `审计过程/评测/`（`test-results.md`、`output-cases.md`、`trigger-suite.json`、`trigger-blind.json`、`test-prompts/`）与 `审计过程/流水线文档/PIPELINE_STATE.md`。
> 测试宿主：ZCode / GLM-5.3；盲测执行者：未参与蒸馏、看不到预期答案与断言的独立子智能体；测试日期 2026-10-24。

## 测试范围

- **skill 数量**：8 个可安装 skill 目录——`single/` 1 个入口（`gann-45-years-skill`）+ `pack/` 7 个入口（`gann-45-years-skill-router` 来源路由 + 6 个已晋级独立 skill）。能力卡共 8 张，其中成交量确认与多空配对两张在 pack 里经 router 到达，不单独成目录。
- **test-prompts 文件**：归档共 9 份（`审计过程/评测/test-prompts/<skill名>.json`），按 skill 名落到各 skill 目录 8 份，1 份（`gann-volume-confirm-skill`）因仓库无同名目录跳过。`evals/test-prompts/` 保留原 9 份副本，未删除。
- **用例总量**：9 份合计 74 条；已落位的 8 份合计 68 条（跳过的那份 6 条）。
- **覆盖类型**（取自 test-prompts JSON 的 `type` 字段）：
  - `should_trigger` 31 条（落位 29 条）——正面触发
  - `should_not_trigger` 26 条（落位 24 条）——诱饵与近邻负例
  - `edge_case` 17 条（落位 15 条）——边界与口径质询
  - `output_case`：test-prompts JSON 中为 0 条。输出类断言单独放在 `evals/output-cases.md`，共 16 个场景（OC-1…OC-8 × 正常/边界），不与触发用例混放。

## 结构检查

本次逐项脚本校验（2026-10-28），结果如实记录：

- **JSON 可解析性**：8 份已落位 test-prompts 全部通过 `json.load`，无语法错误。
- **JSON 字段**：8 份顶层均为 `skill` / `version` / `source` / `test_cases` 四键；68 条用例全部具备 `id` / `type` / `prompt` / `expected_behavior` / `notes`，无缺字段用例。
- **frontmatter**：8 个 `SKILL.md` 全部以 `---` 开头，`name` 与 `description` 齐备。
- **六段完整性**：`bundle/cards/` 下 8 张能力卡全部含 R / I / A1 / A2 / E / B 六段，无缺段。
- **未做**：未做 JSON schema 校验（本包没有正式 schema 文件）；未重算 `BUILD_MANIFEST.json` 的文件哈希——新增的 `test-prompts.json` 与 `candidates/` 不在原编译清单内，哈希未更新。

## 结果

- skills: 8
- test_json: 9（归档口径）／8（已落位）
- 通过情况：本包**未附带针对新增落位 68 条 test-prompts 的逐条评测记录**。阶段 4 实测的是触发盲测集（32 条）与输出评测（16 场景），结果摘自 `evals/test-results.md`，原文如下：

  - **触发精度盲测**：32 条 prompt × 8 项能力——完全命中 30/32，边缘可接受 2 条（t21、t22），错误激活 0；8 条跨能力诱饵全部正确避开。
  - **输出评测**：8 项能力 × 正常/边界 = 16 个场景，16/16 通过，0 失败。
  - **带卡 vs 无卡对照**：16 个场景均跑两版，报告归纳出 5 处关键差异（方法本体交付、口径与单位、边界意识）。
  - **修复记录**：t21 暴露近邻歧义后，摆动图卡 description 增补「只产出图表信号，不做开仓决策与仓位」；无其他回炉项。
  - **如实说明**：t22（「用 3 日均线分析」）判官判为无匹配能力，属防御性合理，未判失败但已记录在案。

## 可接入 darwin-skill 的后续动作

1. **直接作为回归样本池**：68 条用例已按 skill 目录就近存放，每个 skill 目录自带 `test-prompts.json`。改 description 或能力卡后，对同一批用例重跑触发判定即可做回归，不必再从归档取件。
2. **格式已兼容**：用例 `type` 采用 `should_trigger` / `should_not_trigger` / `edge_case` 三分类，是 darwin 兼容格式，无需转换；输出类断言需从 `evals/output-cases.md` 单独解析后接入。
3. **补测缺口**：本次只落位、未评测。建议下一步对 68 条用例做一次全量盲测，把逐条结果补回本文件；跳过的 6 条（`gann-volume-confirm-skill`）在该能力升为独立入口后一并接入。
4. **按模式分组跑**：router 的 `should_not_trigger` 里有 2 条是「应由晋级 skill 直接承接」的近邻负例，single 与 pack 两种模式下的预期行为不同，回归时须按模式分组，不能混跑。
5. **口径重标定提醒**：用例里的点位与点数（如「5 点容差」「9 点摆动」）仍是原书口径，做现代标的回归时应同步补一条重标定断言，避免把 1949 年道指尺度当默认值。
