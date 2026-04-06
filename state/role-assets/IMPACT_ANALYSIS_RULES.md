# workflow_testmate 影响面分析与覆盖规则

## 规则
- 每次改动先判触达模块，再映射到回归组。
- 默认顺序：
  - 先跑命中模块的最小 smoke
  - 再跑跨链路回归
  - 最后决定是否要补浏览器真实验收

## 模块 -> 必跑回归
- `assignment_service_parts/*`
  - 必跑：
    - `TC-ASSIGN-001`
    - `TC-ASSIGN-003`
    - `TC-ASSIGN-004`
    - `TC-ASSIGN-005`
- `schedule_service.py` / `api/schedules.py` / `schedule_center_*`
  - 必跑：
    - `TC-SCH-001`
    - `TC-SCH-002`
    - `TC-SCH-004`
    - `TC-SCH-005`
    - 若触达自迭代逻辑，再加 `TC-AWAKE-*`
- `dashboard.py` / 任务中心顶部状态展示
  - 必跑：
    - `TC-AWAKE-004`
    - `TC-ASSIGN-001`
- `role_creation_service_parts/*`
  - 必跑：
    - `TC-RC-001`
    - `TC-RC-002`
    - `TC-RC-003`
    - `TC-RC-004`
- `defect_service*`
  - 必跑：
    - `TC-DEF-001`
    - `TC-DEF-002`
    - `TC-DEF-003`
- `runtime_upgrade*` / `start_workflow_env.ps1`
  - 必跑：
    - `TC-REL-001`
    - `TC-REL-002`
    - `TC-REL-003`

## 补充规则
- 如果页面入口、状态展示、布局有改动：
  - 默认补真实浏览器 smoke 或至少静态 bundle 语法检查
- 如果生产环境出过同类事故：
  - 该事故对应回归升为强制回归
