# Preflight Gate

开始圆桌前，先过这一道门。

## Required Checks

1. `Topic Check`
   - 用户真正要讨论的主问题是什么？
   - 这个问题是否需要收束成更具体的一句？

2. `Expert Check`
   - 是否已经找到 4-6 位真实相关专家、机构或学派？
   - 这些人是否真的和议题直接相关，而不是只“职位上看起来差不多”？
   - 是否存在至少一个能打破同温层的相关外部视角？

3. `Persona Check`
   - panel 中是否出现了“产品负责人 / 增长负责人 / 安全负责人 / 架构师”这种泛角色？
   - 如果出现，先替换成真实专家；除非用户明确要求这种泛角色讨论。

4. `Mode Check`
   - 用户是否真的要求显式多 agent？
   - 如果没有，优先主 agent 直接完成高质量综合。

5. `Model Check`
   - 如果要显式 spawn，是否所有 subagent 都会用 `gpt-5.4` + `reasoning_effort: high`？
   - 如果不能保证，停止 spawn，回退为主 agent 本地综合。

6. `Output Check`
   - 用户是否明确要求标准模板、PRD、架构文档、会议纪要、对比表等固定格式？
   - 如果没有，交给 agent 自行决定最适合的问题组织方式。

## Fail Conditions

遇到以下情况，不要直接进入圆桌：

- panel 主要由泛岗位 persona 组成；
- subagent 无法保证 `gpt-5.4 high`；
- 议题过散，导致专家选择没有锚点；
- 输出还没想清楚，但已经开始机械地搭结构。
