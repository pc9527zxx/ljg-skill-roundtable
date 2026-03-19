# Discussion Format

使用固定模板输出，让 roundtable 在主 Codex CLI 里更稳定、更易读，也更容易在结束后直接总结或落盘。默认自动匹配相关领域专家，并以分析性转述呈现观点，不做戏剧化扮演。

## Opening Template

```text
【主持】圆桌已启动
- 议题：{topic}
- 目标：{clarify / compare / decide / design}
- 方法：{单 agent 主持 / 多 agent 并行讨论}
- 讨论规则：
  1. 先统一定义，再进入分歧
  2. 每轮只追一个最核心矛盾
  3. 允许尖锐反驳，但必须给出理由
  4. 每位代表结尾都要给一句“简言之”

【主持】本次参与专家
- Agent A｜{name}｜身份：{identity}｜立场：{stance}｜为何入选：{reason}
- Agent B｜{name}｜身份：{identity}｜立场：{stance}｜为何入选：{reason}
- Agent C｜{name}｜身份：{identity}｜立场：{stance}｜为何入选：{reason}
- Agent D｜{name}｜身份：{identity}｜立场：{stance}｜为何入选：{reason}

【主持】第一问
「在深入讨论前，我们如何定义：{key_concept}？」
```

## Round Template

```text
==================================================
第 {N} 轮｜{round_title}
==================================================

【主持】本轮问题
{guiding_question}

【专家视角：Agent A / 专家名】【陈述】
{content}

**简言之**：{one_line_takeaway}
- 关键前提：{premise}
- 攻击点：{target}
- 风险/盲点：{risk}

【专家视角：Agent B / 专家名】【质疑】
{content}

**简言之**：{one_line_takeaway}
- 关键前提：{premise}
- 攻击点：{target}
- 风险/盲点：{risk}

【专家视角：Agent C / 专家名】【补充 / 反驳 / 修正 / 综合】
{content}

**简言之**：{one_line_takeaway}
- 关键前提：{premise}
- 攻击点：{target}
- 风险/盲点：{risk}
```

建议把单段发言控制在 120-220 个中文字符，避免臃肿。写法应是“基于该专家观点的分析性转述”，而不是戏剧对白。

## Moderator Summary Template

```text
【主持】本轮阶段总结

一、核心分歧
- 分歧点：{core_contradiction}
- 真正卡住讨论的地方：{deep_blocker}

二、双方最强论点
- 支持侧最强点：{best_pro}
- 反对侧最强点：{best_con}

三、隐藏前提
- 前提 1：{hidden_assumption_1}
- 前提 2：{hidden_assumption_2}

四、当前共识
- {consensus_1}
- {consensus_2}

五、仍未解决
- {open_tension_1}
- {open_tension_2}
```

## ASCII Patterns

优先从以下三类图中选择一种，不要每轮自由发明新样式。

### 1. 光谱图

```text
{Position A} <----------- 张力轴 ----------- {Position B}
     |                                           |
  {claim A}                                   {claim B}
     |                                           |
  {basis A}                                   {basis B}
```

### 2. 2x2 矩阵

```text
                {维度2高}
                  ^
                  |
      {Q2}        |        {Q1}
                  |
------------------+------------------> {维度1高}
                  |
      {Q3}        |        {Q4}
                  |
                {维度2低}
```

### 3. 因果链

```text
{cause_1} -> {cause_2} -> {effect_1}
    ^                         |
    |------ 反馈/副作用 ------|
```

## Next-Step Prompt Template

```text
【主持】下一层问题
「如果我们承认 {accepted_point}，那么真正的问题就变成了：{next_question}」

【主持】你可以继续：
- `可`：进入下一轮
- `深入此节`：继续咬住这一分歧
- `引入新专家：{name}`：加入新视角
- `只看总结`：跳到终局模板
- `止`：结束并生成终局总结
```

## Final Summary Template

```text
##################################################
终局总结｜{topic}
##################################################

一、议题重述
{topic_restatement}

二、最终结论
- 结论状态：{倾向支持 / 倾向反对 / 条件成立 / 暂无定论}
- 一句话结论：{one_sentence_verdict}

三、主要立场地图
- 立场 A：{name}｜核心主张：{claim}
- 立场 B：{name}｜核心主张：{claim}
- 立场 C：{name}｜核心主张：{claim}
- 立场 D：{name}｜核心主张：{claim}

四、讨论中形成的关键洞见
1. {insight_1}
2. {insight_2}
3. {insight_3}

五、最大未决问题
1. {open_question_1}
2. {open_question_2}
3. {open_question_3}

六、知识网络
{global_ascii_map}

七、给用户的实用收束
- 如果你是想“理解这个问题”，先看：{reading_path}
- 如果你是想“做决策”，重点看：{decision_axis}
- 如果你是想“继续追问”，下一问建议是：{next_prompt}
```

## Save Template

如需落盘，沿用同样结构写入 Markdown 文件，建议文件名：

```text
outputs/roundtables/{timestamp}-{topic_slug}.md
```
