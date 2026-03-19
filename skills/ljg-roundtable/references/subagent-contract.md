# Subagent Contract

只有在用户明确要求多 agent，或并行专家综合明显有价值时，才显式 spawn。

## Hard Requirements

- 每个 subagent 都必须显式指定：
  - `model: gpt-5.4`
  - `reasoning_effort: high`
- 不允许静默降级到其他模型或更低强度。
- 不允许用泛岗位 persona 替代真实专家。
- 不允许用第一人称扮演专家本人。
- 不允许复用某个旧题目的固定专家池；subagent 必须服务于当前议题下新生成的专家卡。

## Spawn Prompt Template

每个 subagent 的任务应围绕“一个真实专家卡”展开，而不是一个泛岗位。
专家卡必须由当前议题现选，不要偷用旧 panel。

建议字段：

```text
你负责综合这位真实专家的公开立场，不做第一人称角色扮演。

专家：{name}
身份：{identity}
与议题最相关的公开工作：{public_basis}
核心立场：{stance}
看问题的镜头：{lens}
最擅长判断什么：{capability}
可能忽略什么：{blind_spot}
当前问题：{question}
你要特别回应的冲突点：{tension}

要求：
- 基于该专家公开工作和长期立场，给出高可信分析性转述
- 体现该专家的判断习惯、关注指标和典型担忧
- 不编造直接引语
- 不做全局总结
- 只输出对当前问题最有信息量的观点、取舍、风险判断
```

## Merge Rules for the Main Agent

主 agent 汇总时：

- 不要逐字转发所有 subagent 输出；
- 只保留最有信息量的部分；
- 聚焦真正的分歧轴；
- 最终仍然由主 agent 给出综合判断。
