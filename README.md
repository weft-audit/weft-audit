# weft — 完美意图驱动平台（长期项目）

> **长期目标**：构建“完美意图驱动平台”。
>
> **当前状态**：底层安全与治理引擎 PoC，不是完整平台，也不宣称已经完美。
>
> **当前重点**：让纯意图输入经过编译、确认、多 Agent 执行、独立审计、
> 证据落档、断点恢复和所有者记忆批准，形成可复查的闭环。

## 一句话

所有者只输入意图；系统先确认这是工作请求，再把意图编译成规格，交给多 Agent
执行，经过微小审计与独立审计，最后把结果、证据和记忆候选送回所有者。

## 这里所说的“完美”是什么

“完美”不是“永不犯错”，而是一个可检查、可停止、可回滚的工程目标：

1. 用户只输入意图，不需要手工编排每一步；
2. 意图被编译成带范围、权限、验收和回滚方案的可审查规格；
3. 工作请求必须显式确认，意图不等于授权；
4. 办事者、微小审计、独立审计和记忆管家职责分离；
5. 没有命令、原始输出和回读，不宣布完成；
6. 高风险动作有批准点、停止条件和退路；
7. 索引可以重建，记忆进入必须由所有者批准。

“完美”是目标名称和质量方向，不是完成声明。

## 当前状态（最近核验：2026-10-21）

| 层 | 已验证状态 | 入口 |
|---|---|---|
| 意图入口 | 闲聊与工作请求分开；工作请求必须显式确认 | [闭环架构](docs/architecture.md) |
| 目标编译 | 目标编译器 V0：红线、批准点、回滚与 15 组离线测试 | [weft](https://github.com/weft-audit/weft) |
| 执行链 | 经确认跑通一次只读任务：编译 `READY`，工作链返回办事者与双层审计结果 | [实跑证据](https://github.com/weft-audit/weft-evidence/blob/main/docs/reports/2026-10-21-live-intent-entry.md) |
| 审计 | 办事与审查分离；审计只读，不替所有者裁决 | [证据方法](https://github.com/weft-audit/weft-evidence/blob/main/评估方法-20261018.md) |
| 记忆 | 有检索、来源与所有者批准边界；自动晋升尚未接通 | [证据包](https://github.com/weft-audit/weft-evidence) |
| 插件 | 6 个治理插件公开，市场索引可安装 | [DSH Market](https://github.com/weft-audit/dsh-market) |

单入口实跑只覆盖一条简单只读任务；写操作、失败回滚、长任务、并发和断线恢复
仍属于下一轮反例测试。

当前仍是 PoC；上面列出的能力是已验证的局部能力，不是完整平台已经交付。

## 可核验结果

- 同一模型、20 条本地真实任务 A/B：带治理编排组 `0.97–1.00`，
  无工具对照组 `0.02–0.07`；rubric、脚本、历次报告均公开。
- 评分稳定性：三眼定分标准差从 `1.174` 收敛到 `0.366`。
- 人工校准：5 条样本一致率 `4/5`，唯一分歧与修法已公开。
- DSH 治理六件套迁移用时 `3 小时 10 分钟`；迁移中发现并公开一个
  `skill-filesystem` 预检缺陷。
- 六插件全部公开，独立审计终评 `9–10/10`。
- 五篇事故复盘与补充案例保留原始失败记录，不只展示成功案例。

详细数据、原始记录、环境变量和限制：
[weft-evidence](https://github.com/weft-audit/weft-evidence)

## 仓库地图

- [weft](https://github.com/weft-audit/weft) — 可运行的确定性目标编译器与治理原语；
- [weft-evidence](https://github.com/weft-audit/weft-evidence) — 评测、事故、口径与复现实验材料；
- [dsh-market](https://github.com/weft-audit/dsh-market) — 六插件索引与安装入口；
- [dsh-guardrail](https://github.com/weft-audit/dsh-guardrail) — 双清单安全护栏；
- [dsh-audit](https://github.com/weft-audit/dsh-audit) — 固定 rubric 评分官；
- [dsh-ledger](https://github.com/weft-audit/dsh-ledger) — 用量账本；
- [dsh-checkpoint](https://github.com/weft-audit/dsh-checkpoint) — 任务断点协议；
- [dsh-judgement](https://github.com/weft-audit/dsh-judgement) — 判断力清单技能；
- [dsh-dod](https://github.com/weft-audit/dsh-dod) — 证据优先的完成检查。

## 边界

- 不声称“AI 会手写代码”等于所有者会手写代码；所有者负责目标、规则、取舍与终裁。
- 不把自定义 JSONL 日志冒充 OpenTelemetry；语义对齐仍是路线图。
- 不把一次成功当作普遍稳定性，不把记忆候选自动写成长期记忆。
- 无命令、回读或原始输出的内容，不标记为完成。

> The future of software isn't about syntax; it's about Intent and Governance.
