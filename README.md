# ljg-skill-roundtable

一个更像“专家技能”而不是“角色扮演提示词”的圆桌 skill。

它的目标不是把讨论写得热闹，而是把问题讲深：自动找相关专家、控制 panel 质量、必要时并行综合、最后给出高质量判断。

## 这个 skill 现在怎么工作

- 用户只在主 Codex CLI 提问
- 主 agent 自动寻找相关真实专家、机构或学派
- 默认不做戏剧化角色扮演，只做高可信专家观点综合
- 只有用户明确要求多 agent / 并行讨论时，才显式 spawn subagent
- 显式 subagent 默认必须使用 `gpt-5.4` + `high`
- 输出格式默认由 agent 自己决定；只有用户明确要求固定模板时，才套模板

## 适合的场景

- 战略问题
- 技术 / 架构问题
- 产品路线和平台设计
- 争议议题的多视角分析
- 需要专家分歧和综合判断的问题

## 触发示例

```text
圆桌会议 自由意志是否存在？
圆桌会议 用多agent讨论这个问题。
圆桌会议 如何设计一个长期可持续的平台？
自动找相关专家来讨论这个问题，不要角色扮演。
```

如果你的环境支持显式 skill 调用，也可以这样说：

```text
Use $ljg-roundtable to analyze this topic with relevant real experts.
Use $ljg-roundtable with gpt-5.4 high subagents and real domain experts.
```

## 仓库结构

- `skills/ljg-roundtable/SKILL.md`：主技能说明
- `skills/ljg-roundtable/agents/openai.yaml`：UI 元数据与默认 prompt
- `skills/ljg-roundtable/references/preflight-gate.md`：开始前的硬检查
- `skills/ljg-roundtable/references/expert-selection.md`：专家选择规则
- `skills/ljg-roundtable/references/subagent-contract.md`：多 agent 执行契约
- `skills/ljg-roundtable/references/output-modes.md`：仅在用户要求模板时使用

## 设计原则

- 专家优先，不用泛角色凑 panel
- 议题优先，不复用某个领域的固定明星 panel
- 不只报名字，要介绍专家是谁、为何相关、会怎么观察问题
- 执行强约束，输出弱约束
- 不角色扮演，只做高可信综合
- 需要并行时再并行，不为热闹而 spawn
- 多 agent 时锁定 `gpt-5.4` + `high`

## License

MIT
