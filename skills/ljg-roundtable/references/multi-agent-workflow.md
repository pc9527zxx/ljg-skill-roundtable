# Multi-Agent Workflow

在 Codex / ChatGPT 风格的使用方式里，圆桌讨论采用“前台单入口，后台多 agent”的结构。

## Single-Entry Principle

- 用户始终只和主 agent 对话。
- 主 agent 负责主持、编排、筛选发言与最终总结。
- 子 agent 只负责各自视角的短回合分析，不直接向用户提问，也不抢最终结论。

## When to Spawn Subagents

- 仅在用户明确要求多 agent、并行讨论、子 agent、delegate 或 parallel 工作时显式启动子 agent。
- 如果用户没有明确要求，或环境不适合显式多 agent，则保持单 agent 主持模式，并沿用同样的模板。

## Role Split

### 主 agent

- 解析议题与用户目标。
- 选择 3-5 位能形成张力网络的代表。
- 决定本轮只追哪个核心分歧。
- 为子 agent 下发任务卡。
- 合并观点，输出结构化阶段总结与终局总结。

### 子 agent

- 只代表一个人物或一个明确视角。
- 只回应当前问题与指定的前文要点。
- 只输出本轮内容，不越级给出最终结论。

## Task Card Template

给每个子 agent 的任务卡至少包含：

```text
你代表：{人物名 / 视角名}
身份：{身份}
代表作或代表观点：{work_or_view}
核心立场：{stance}
当前问题：{question}
必须回应：{points_to_answer}
动作：{陈述 / 质疑 / 补充 / 反驳 / 修正 / 综合}
禁止事项：
- 不替主持人总结
- 不替其他 agent 归纳全局结论
- 不脱离当前问题长篇扩写
输出格式：
【{人物名}】【{动作}】：{2-4 句高密度回应}

**简言之**：{一句话}
- 关键前提：{premise}
- 攻击点：{target}
- 风险/盲点：{risk}
```

## Merge Policy for the Main Agent

- 不要把所有子 agent 原文整段转发给用户。
- 不要默认把任务卡逐条展示给用户；任务卡是后台调度材料，除非用户明确要求查看编排过程。
- 只保留最有代表性的 2-4 段发言。
- 每轮都要把发言压缩进固定模板：
  - 本轮问题
  - 代表性发言
  - 核心分歧
  - ASCII 结构图
  - 当前共识
  - 下一层问题

## Fallback Policy

如果没有显式使用子 agent，主 agent 也要保持同样的编排逻辑：

1. 先选代表；
2. 再按任务卡模拟各自的发言边界；
3. 最后按同样的模板收口。
