# 任务运行输出精简经验

## 适用范围
- 任务中心真实执行 trace
- 节点详情里的运行批次展示
- `stdout/stderr/events` 体积控制与 token 成本收口

## 稳定经验
- 任务中心运行详情不要默认回传 `prompt/stdout/stderr/result` 全文。后端应只回预览文本，并附“已截断 + 引用路径”提示；完整内容留给磁盘引用路径按需查看。
- `stdout/stderr/events.log` 这类 trace 文件要加体积上限，否则一次长输出就会同时拖慢落盘、详情接口和前端渲染。当前验证过的保守上限可先用：
  - `stdout.txt`: `96KB`
  - `stderr.txt`: `96KB`
  - `events.log`: `128KB`
- `events.log` 不能直接把 stdout 事件里的整段 JSON detail 原样写回去；应先做 detail 压缩，只保留有限层级、有限字段和有限字符串长度。
- 前端标题要明确写成“预览”，不要继续标“完整提示词/最终结果”，否则用户会误以为当前面板看到的就是全文。

## 已踩过的坑
- 坑 1：只压接口、不压磁盘 trace，会让页面轻一点，但 `stdout.txt/events.log` 还是继续膨胀，慢问题和存储问题都没真正收口。
  - 避免方式：同时做“落盘上限 + 接口预览”双收口。
- 坑 2：把 `events.log` 复用到带时间戳的普通文本 append helper，会破坏 JSONL 结构，后续 tail/解析全部失效。
  - 避免方式：`events.log` 单独走 raw append；可以限体积，但不能额外包时间戳前缀。
