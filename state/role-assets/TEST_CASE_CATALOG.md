# workflow_testmate 当前项目用例清单

## 使用规则
- 这是当前 `workflow` 的项目级测试清单。
- 每次新功能进入代码根仓后，要补一条或多条用例到对应模块。
- 每次改动前，先按 `IMPACT_ANALYSIS_RULES.md` 选中需要回归的用例组。

## 1. 任务中心
- `TC-ASSIGN-001`
  - 目标：全局主图可加载，节点状态与调度状态可见。
  - 覆盖：`/api/assignments`、`/api/assignments/<ticket>/graph`
- `TC-ASSIGN-002`
  - 目标：新建任务后进入正确状态，依赖关系可见。
  - 覆盖：建单、优先级、依赖、图刷新
- `TC-ASSIGN-003`
  - 目标：`dispatch-next` 后节点进入 `running`，产生 run 证据。
  - 覆盖：调度、执行、run 文件、状态回写
- `TC-ASSIGN-004`
  - 目标：任务失败后可重跑、可人工改状态、可继续回归。
  - 覆盖：失败治理、`rerun`、`override-status`
- `TC-ASSIGN-005`
  - 目标：执行链路详情可见，`stdout/stderr/result/events` 预览不拖垮页面。
  - 覆盖：详情页、输出精简、引用路径

## 2. 定时任务
- `TC-SCH-001`
  - 目标：计划列表和详情可正常展示。
  - 覆盖：`/api/schedules`、详情页、规则摘要
- `TC-SCH-002`
  - 目标：计划命中后向任务中心建单。
  - 覆盖：`scan`、去重、建单、task ref 回写
- `TC-SCH-003`
  - 目标：同一分钟多规则命中只建一次单。
  - 覆盖：dedupe、trigger instance
- `TC-SCH-004`
  - 目标：计划详情能显示最新结果与关联任务。
  - 覆盖：`last_result_*`、`recent_triggers`、`related_task_refs`
- `TC-SCH-005`
  - 目标：中文计划名、摘要、清单、完成标准不乱码。
  - 覆盖：编码链、前后端展示

## 3. 自迭代 / 持续唤醒
- `TC-AWAKE-001`
  - 目标：自迭代计划命中后能自动建出 `workflow` 节点。
  - 覆盖：`source_schedule_id`、`trigger_instance_id`
- `TC-AWAKE-002`
  - 目标：节点能自动派发起跑。
  - 覆盖：schedule -> assignment dispatch
- `TC-AWAKE-003`
  - 目标：smoke 基线未通过时，安全闸口能阻止继续放量。
  - 覆盖：guard / fail-closed / 降级开关
- `TC-AWAKE-004`
  - 目标：24h 连续运行目标在网页可见。
  - 覆盖：dashboard / 任务中心工作状态看板

## 4. 角色创建
- `TC-RC-001`
  - 目标：角色创建会话可启动、可推进阶段。
- `TC-RC-002`
  - 目标：角色创建后台任务能生成并回显。
- `TC-RC-003`
  - 目标：异步删除 / 清理语义稳定。
- `TC-RC-004`
  - 目标：分析回复与 UI 中文不乱码。

## 5. 缺陷中心
- `TC-DEF-001`
  - 目标：短描述缺陷可正常受理，不因字数少被误驳回。
- `TC-DEF-002`
  - 目标：缺陷优先级、任务命名、全局主图引用正确。
- `TC-DEF-003`
  - 目标：缺陷可路由到 `workflow_bugmate`，回归后结果可追踪。

## 6. 发布与运行
- `TC-REL-001`
  - 目标：`prod` supervisor 托管升级链路正常。
- `TC-REL-002`
  - 目标：`healthz`、instance、manifest 三处状态一致。
- `TC-REL-003`
  - 目标：重启后关键链路可恢复，不遗留卡死态。
