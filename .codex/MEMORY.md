# 工作区记忆规范

## 目的
- 本文件是当前工作区的顶层记忆规范。
- 具体轮次总结不要写在这里，只写入每日日记文件。
- 把 `.codex/` 视为 agent 记忆和内部指导，不得当成产品运行态。

## 角色工作区适用口径
- 通过“创建角色”生成的新 agent 工作区，默认沿用这套记忆库结构与归档规范。
- 角色工作区的 `AGENTS.md` 必须显式引用 `.codex/MEMORY.md`，并把它作为日切、月切、经验读取与日记追加的真相源。
- 若角色工作区缺少记忆骨架、经验索引或归档汇总，优先使用 `python scripts/manage_codex_memory.py repair-rollups --root .` 修复。

## 必读顺序
1. `AGENTS.md`
2. `.codex/experience/index.md`
3. 读取 `.codex/experience/index.md` 中“必读经验”列出的经验文件
4. `.codex/SOUL.md`
5. `.codex/USER.md`
6. `.codex/MEMORY.md`
7. `.codex/memory/全局记忆总览.md`
8. `.codex/memory/YYYY-MM/记忆总览.md`
9. `.codex/memory/YYYY-MM/YYYY-MM-DD.md`

## 目录模型
- 经验索引：`.codex/experience/index.md`
- 经验卡：`.codex/experience/*.md`
- 全局总览：`.codex/memory/全局记忆总览.md`
- 月度总览：`.codex/memory/YYYY-MM/记忆总览.md`
- 每日日记：`.codex/memory/YYYY-MM/YYYY-MM-DD.md`

## 写入规则
- 经验卡只记录可复用模式、踩坑与规避规则；不要写成逐轮流水账。
- 出现新的稳定经验时，更新对应 `.codex/experience/*.md`，并同步维护 `index.md`。
- 每轮工作结束后，都要向当日日记追加一条带时间戳的总结。
- 每日日记条目默认使用第一人称，写成“我今天 / 我这轮 / 我刚刚确认到”的日记口吻；在不牺牲可检索性的前提下，允许保留一点当时的观察和状态。
- 每日日记条目优先使用结构化回忆格式：`主题`、`背景`、`动作`、`结论`、`验证`、`产物`、`下一步`；必要时可补一行 `感受/观察`。
- 当日总结只保留在当日日记中，直到次日开始。
- 当月总览只归档截至昨日的日级摘要。
- 全局总览只归档已闭月的月度总结。

## 每日条目字段说明
- `主题`：我这轮主要在做什么。
- `背景`：我为什么开始处理这件事，包括触发原因或发现的缺口。
- `动作`：我实际改了什么、创建了什么、迁移了什么、检查了什么。
- `结论`：我确认下来的规则、判断或会影响后续工作的结论。
- `验证`：我执行过的命令、检查项和观察结果。
- `产物`：我这轮触达的关键文件或目录。
- `下一步`：我接下来还要跟进什么、延后检查什么、满足什么条件后再归档。
- `感受/观察`：可选，用来补一句当时最值得保留的直觉、风险感受或现场状态，但不要写成大段抒情。
- 条目保持简洁，但要完整到让我或后续读者不用重新打开大量无关文件也能复原本轮工作。

## 归档检查
- 日切检查：新一天首轮工作前，确认昨日日记已汇总到对应月度总览。
- 月切检查：新一月首轮工作前，确认上月总览已汇总到全局总览。
- 如果发现必须的总览条目缺失，先补归档，再继续正常工作。

## 验证命令
- `python scripts/manage_codex_memory.py status --root .`
- `python scripts/manage_codex_memory.py verify-rollups --root .`
- `python scripts/manage_codex_memory.py repair-rollups --root .`
- `python scripts/manage_codex_memory.py append --root . --summary "<round summary>"`
- `python scripts/manage_codex_memory.py append --root . --topic "<topic>" --context "<context>" --actions "<action1|action2>" --decisions "<decision1|decision2>" --validation "<check1|check2>"`
