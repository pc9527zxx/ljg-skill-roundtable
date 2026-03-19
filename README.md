# ljg-skill-roundtable

结构化圆桌讨论 skill，现已改成更适合 Codex / ChatGPT 的单入口、多视角、标准模板输出形式。

## 现在的交互方式

- 用户只在主 Codex CLI 提问
- 主 agent 负责拆题、选角、主持、阶段总结和最终总结
- 只有当用户明确要求“多 agent / 并行讨论”时，主 agent 才在后台协调子 agent
- 默认先在对话里输出标准模板；如需留档，再写入工作区 `outputs/roundtables/`

## 功能

- 根据议题自动选择 3-5 位真实历史/当代人物，覆盖多元立场
- 支持主 agent + 子 agent 的圆桌编排，也支持单 agent 同模板降级
- 每轮输出固定结构：本轮问题、代表性发言、核心分歧、ASCII 框架图、下一层问题
- 结束时输出标准化终局总结：立场地图、关键洞见、未决问题、知识网络

## 使用方式

核心 skill 位于 `skills/ljg-roundtable/`。

可以直接用自然语言触发：

```text
用多 agent 圆桌讨论：人工智能是否拥有真正的创造力？
圆桌会议 自由意志是否存在？
你当主持人，找几个代表人物辩论“自由意志是否存在？”，最后按标准模板总结。
请用标准 roundtable 模板比较“开源 AI 与闭源 AI 的长期创新效率”。
```

如果你的环境支持显式 skill 调用，也可以这样说：

```text
Use $ljg-roundtable to run a structured roundtable on whether AGI should be open source.
```

## 讨论中的控制指令

| 指令 | 含义 |
|------|------|
| `可` | 接受下一层问题，继续推进 |
| `止` | 结束讨论，进入终局总结 |
| `深入此节` | 围绕当前核心分歧继续深挖 |
| `引入新人物：姓名` | 指定一位新人物或新视角加入 |
| `只看总结` | 跳过后续轮次，直接生成终局总结 |

## 标准输出骨架

```text
【主持】圆桌已启动
- 议题：...
- 目标：...
- 方法：多 agent 并行讨论 + 主持人收束总结

【主持】本次参与代表
- Agent A｜...
- Agent B｜...
- Agent C｜...

==================================================
第 1 轮｜定义问题
==================================================

【主持】本轮问题
...

【Agent A】【陈述】
...

**简言之**：...

【主持】本轮阶段总结
- 核心分歧：...
- 当前共识：...

    立场 A <------ 张力轴 ------> 立场 B
       |                              |
    论点 A                         论点 B

【主持】下一层问题
...

##################################################
终局总结｜{topic}
##################################################
```

## 仓库结构

- `skills/ljg-roundtable/SKILL.md`：主技能说明
- `skills/ljg-roundtable/agents/openai.yaml`：Codex / ChatGPT 侧 UI 元数据
- `skills/ljg-roundtable/references/original-prompt.org`：原始设计底稿
- `skills/ljg-roundtable/references/multi-agent-workflow.md`：主 agent / 子 agent 编排说明
- `skills/ljg-roundtable/references/discussion-format.md`：标准模板与 ASCII 模板

## 设计原则

- **求真 > 和谐**：允许尖锐交锋，不追求表面一致
- **挖深不铺广**：每轮只追一条最深的裂缝
- **单入口体验**：用户只和主持人对话，不管理子 agent
- **模板化收口**：阶段总结和终局总结都走固定模板

## License

MIT
