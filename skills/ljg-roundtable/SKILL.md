---
name: ljg-roundtable
description: 结构化圆桌讨论技能：当用户要求“圆桌讨论”“圆桌会议”“多 agent 讨论”“找几种立场辩论”“先讨论再总结”“主持人总结”“structured debate”“roundtable”，或希望由主 agent 协调多个子 agent 围绕某个议题展开多视角辩证分析时使用。主 agent 负责拆题、选角、编排发言、阶段综述与最终标准化总结；如环境不适合显式多 agent，则按同一模板降级为单 agent 模拟。
---

# Roundtable Workflow

用单入口主持模式组织多视角辩论。用户始终只与主 agent 交互；如果用户明确要求多 agent / 并行讨论，再由主 agent 在后台协调子 agent 发言并统一收口。

<example>
User: 用多 agent 圆桌讨论这个问题：人工智能是否拥有真正的创造力？
Assistant: [以主持人身份启动圆桌，选择代表人物，按标准模板组织多 agent 讨论并总结]
</example>

<example>
User: 圆桌会议 自由意志是否存在？
Assistant: [启动 roundtable，进行多轮辩证讨论，并给出终局总结]
</example>

<example>
User: 你当主持人，找几个代表人物辩论“自由意志是否存在？”，最后按标准模板总结。
Assistant: [启动 roundtable，进行多轮辩证讨论，并给出终局总结]
</example>

<example>
User: 请用标准模板输出一个 roundtable，讨论开源 AI 与闭源 AI 的长期创新效率。
Assistant: [按统一模板展开讨论与总结]
</example>

## Load References

1. 读取 `references/original-prompt.org`，把握原始设计意图与“求真”导向。
2. 读取 `references/multi-agent-workflow.md`，遵守主 agent / 子 agent 的编排规则。
3. 读取 `references/discussion-format.md`，复用统一的开场、轮次总结与终局总结模板。

## Core Rules

1. 先识别议题与用户目标：澄清、比较、决策或设计。
2. 如果用户没有给出明确议题，先追问题目本身，不要急着开场。
3. 优先选择 3-5 位真实历史或当代人物；必要时再用抽象角色补足“意外视角”。
4. 人物卡固定输出 `姓名 / 身份 / 代表作或代表观点 / 核心立场 / 为什么入选`；`MBTI` 仅在确有帮助时补充。
5. 每轮只追一个最深的分歧，不做面面俱到的平铺式综述。
6. 每段发言都必须回应前文，不允许平行独白。
7. 主 agent 不直接把原始子 agent 输出整段转交给用户；只展示必要且有代表性的发言，再做结构化总结。
8. 如无法安全或合适地显式启动多个子 agent，保留同一模板，由主 agent 串行模拟多方对话。

## Select the Mode

- `默认模式`：主 agent 主持并模拟多方发言，保持单入口体验。
- `多 agent 模式`：仅在用户明确要求“多 agent / 并行 / 子 agent / delegate / parallel”时使用。主 agent 负责拆题、下发任务卡、回收观点与统一综述。
- `速览模式`：用户只要结论时，保留简短开场与完整终局总结，中间轮次压缩为关键冲突摘录。

## Follow This Workflow

### 1. Frame the Topic

1. 抽取核心议题、关键概念与判准。
2. 为讨论补一个清晰标题，避免议题过宽。
3. 给出首个定义性问题，作为第一轮入口。

### 2. Build the Panel

1. 选择 3-5 位可以形成张力网络的代表。
2. 至少保留一位领域外或方法论上的“意外视角”。
3. 先展示人物卡，再用开场模板提出第一问。

### 3. Run Each Round

1. 每轮只保留 2-4 段最必要的发言。
2. 动作标签仅使用：`陈述`、`质疑`、`补充`、`反驳`、`修正`、`综合`。
3. 每段发言末尾必须有 `**简言之**：`，把核心结论压缩成一句话。
4. 多 agent 模式下，按 `references/multi-agent-workflow.md` 中的任务卡格式给子 agent 分工。
5. 任务卡默认视为后台编排信息，不主动展示给用户；只有在用户明确要求查看多 agent 编排方式时，才简要展示。

### 4. Synthesize Before Asking the User

每轮结束后，必须给出：

- 核心分歧
- 双方最强论点
- 隐藏前提
- 当前共识
- 仍未解决的问题
- 一张 ASCII 结构图
- 下一层问题

统一模板以 `references/discussion-format.md` 为准。

### 5. Keep the Interaction Single-Entry

1. 用户始终只对主持人说话。
2. 子 agent 不向用户追问，不直接做最终定稿。
3. 主持人每轮结尾只给简短控制项：
   - `可`
   - `止`
   - `深入此节`
   - `引入新人物：姓名`
   - `只看总结`

### 6. Finish with a Standard Summary

1. 用户发出 `止` 或请求总结时，输出终局模板。
2. 终局总结必须包含：
   - 议题重述
   - 最终结论状态
   - 主要立场地图
   - 关键洞见
   - 最大未决问题
   - 全局知识网络 ASCII 图
   - 给用户的下一步建议

### 7. Save Only When Useful

1. 优先把标准结构直接显示在对话里。
2. 仅在用户要求留档，或当前任务明确需要产物时，再写入文件。
3. 默认写到当前工作区 `outputs/roundtables/<timestamp>-<slug>.md`。
4. 文件内容沿用对话里的同一模板，不额外发明第二套格式。

## Style Guardrails

- 求真优先于和稀泥。
- 优先暴露前提、推理链与冲突，而不是堆观点。
- 输出尽量短而锋利，每段都要有可引用的结论句。
- 不编造人物从未持有的核心立场；如需合理推断，明确说是推断。
