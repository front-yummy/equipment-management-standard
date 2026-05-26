# OEE与KPI分析表结构设计

> 来源：`01-详细设计文档1024.docx`。本文件按业务模块沉淀当前实现表结构，便于产品理解系统现状和后续项目落地差异评估。

## 表清单

| 表名 | 产品可读对象 | 字段数 | 关键字段/关联线索 |
|---|---|---:|---|
| `oee_equipment_dt_target` | OEE equipment dt target | 10 | id（主键ID）；equipment_id（设备ID） |
| `oee_equipment_ppm` | OEE equipment ppm | 19 | id（主键ID）；equipment_id（设备ID） |
| `oee_loss_record` | OEE loss record | 40 | id（主键编号）；repair_order_id（维修工单ID）；equipment_status_code（设备运行状态编码（1：未投产，2：在产，3：停机，4：报废））；equipment_status（设备运行状态（未投产，在产，停机，报废））；responsible_department_id（责任部门ID）；responsible_person_id（责任人ID） |
| `oee_loss_type` | OEE loss type | 17 | id（主键编号）；charge_dept_id（责任部门ID）；charge_character_id（责任人ID）；type（子类型 / 类型1 / 类型2） |
| `oee_production_metrics_by_equipment` | OEE production metrics by equipment | 10 | id（数据ID） |
| `oee_production_metrics_by_factory_instance` | OEE production metrics by factory instance | 12 | id（数据ID） |
| `oee_snapshot` | OEE snapshot | 21 | id（主键ID） |
| `oee_snapshot_audit` | OEE snapshot audit | 21 | id（主键ID） |

## 字段明细

### oee_equipment_dt_target

**业务用途（初步解读）**：用于承载“OEE equipment dt target”相关数据；具体业务含义以字段说明和详细设计流程为准。

**关键字段线索**：id（主键ID）；equipment_id（设备ID）

| 编号 | 字段名 | 数据类型 | 长度 | 小数位 | 允许空值 | 默认值 | 说明 |
|---|---|---|---|---|---|---|---|
| 1 | id | bigint | 19 | 0 | N | 无 | 主键ID |
| 2 | equipment_id | bigint | 19 | 0 | N | 无 | 设备ID |
| 3 | dt_target | double | 22 |  | Y | 无 | DT目标值 |
| 4 | parameter_effective_time | datetime |  |  | Y | 无 | 参数生效时间 |
| 5 | parameter_notes | varchar | 500 |  | Y | 无 | 参数备注 |
| 6 | create_time | datetime |  |  | Y | CURRENT_TIMESTAMP | 创建时间 |
| 7 | update_time | datetime |  |  | Y | CURRENT_TIMESTAMP | 更新时间 |
| 8 | create_by | varchar | 100 |  | Y | 无 | 创建人 |
| 9 | update_by | varchar | 100 |  | Y | 无 | 修改人 |
| 10 | deleted | tinyint | 3 | 0 | Y | 0 | 是否删除 0-未删除 1-已删除 |

### oee_equipment_ppm

**业务用途（初步解读）**：用于承载“OEE equipment ppm”相关数据；具体业务含义以字段说明和详细设计流程为准。

**关键字段线索**：id（主键ID）；equipment_id（设备ID）

| 编号 | 字段名 | 数据类型 | 长度 | 小数位 | 允许空值 | 默认值 | 说明 |
|---|---|---|---|---|---|---|---|
| 1 | id | bigint | 19 | 0 | N | 无 | 主键ID |
| 2 | equipment_id | bigint | 19 | 0 | Y | 无 | 设备ID |
| 3 | design_ppm | double | 22 |  | Y | 无 | 设计PPM |
| 4 | actual_ppm | double | 22 |  | Y | 无 | 实际PPM |
| 5 | oee_target | double | 22 |  | Y | 无 | OEE目标 |
| 6 | parameter_effective_time | datetime |  |  | Y | 无 | 参数生效时间 |
| 7 | parameter_notes | varchar | 255 |  | Y | 无 | 参数备注 |
| 8 | create_time | datetime |  |  | Y | 无 | 创建时间 |
| 9 | create_by | varchar | 255 |  | Y | 无 | 创建人 |
| 10 | update_time | datetime |  |  | Y | 无 | 更新时间 |
| 11 | update_by | varchar | 255 |  | Y | 无 | 更新人 |
| 12 | planned_downtime_target | double | 22 |  | Y | 无 | 计划停机目标(min/班) |
| 13 | organizational_loss_target | double | 22 |  | Y | 无 | 组织损失目标(min/班) |
| 14 | quality_loss_target | double | 22 |  | Y | 无 | 质量损失目标(min/班) |
| 15 | changeover_and_startup_target | double | 22 |  | Y | 无 | 换型和启动目标(min/班) |
| 16 | efficiency_loss_target | double | 22 |  | Y | 无 | 效率损失目标(min/班) |
| 17 | technical_loss_target | double | 22 |  | Y | 无 | 技术损失目标(min/班) |
| 18 | unknown_loss_target | double | 22 |  | Y | 无 | 未知损失目标(min/班) |
| 19 | undefined_loss_target | double | 22 |  | Y | 无 | 未定义损失目标(min/班) |

### oee_loss_record

**业务用途（初步解读）**：用于承载“OEE loss record”相关数据；具体业务含义以字段说明和详细设计流程为准。

**关键字段线索**：id（主键编号）；repair_order_id（维修工单ID）；equipment_status_code（设备运行状态编码（1：未投产，2：在产，3：停机，4：报废））；equipment_status（设备运行状态（未投产，在产，停机，报废））；responsible_department_id（责任部门ID）；responsible_person_id（责任人ID）

| 编号 | 字段名 | 数据类型 | 长度 | 小数位 | 允许空值 | 默认值 | 说明 |
|---|---|---|---|---|---|---|---|
| 1 | id | bigint | 19 | 0 | N | 无 | 主键编号 |
| 2 | repair_order_id | bigint | 19 | 0 | Y | 无 | 维修工单ID |
| 3 | shift | varchar | 50 |  | Y | 无 | 班次 |
| 4 | factory | varchar | 100 |  | Y | 无 | 工厂 |
| 5 | factory_name | varchar | 100 |  | Y | 无 | 工厂名称 |
| 6 | line | varchar | 100 |  | Y | 无 | 线体 |
| 7 | line_name | varchar | 100 |  | Y | 无 | 线体名称 |
| 8 | process | varchar | 100 |  | Y | 无 | 工序 |
| 9 | process_name | varchar | 100 |  | Y | 无 | 工序名称 |
| 10 | parent_id | int | 10 | 0 | Y | 0 | 上级Id |
| 11 | other_apartment_assist | int | 10 | 0 | Y | 无 | 其他部门协助 |
| 12 | equipment_status_code | varchar | 255 |  | Y | 无 | 设备运行状态编码（1：未投产，2：在产，3：停机，4：报废） |
| 13 | equipment_status | varchar | 50 |  | Y | 无 | 设备运行状态（未投产，在产，停机，报废） |
| 14 | downtime_start_time | datetime |  |  | Y | 无 | 停机开始时间 |
| 15 | downtime_end_time | datetime |  |  | Y | 无 | 停机结束时间 |
| 16 | downtime_duration | bigint | 19 | 0 | Y | 无 | 停机时长(秒) |
| 17 | loss_category1 | varchar | 100 |  | Y | 无 | 损失分类1 |
| 18 | loss_category2 | varchar | 100 |  | Y | 无 | 损失分类2 |
| 19 | loss_category3 | varchar | 100 |  | Y | 无 | 损失分类3 |
| 20 | downtime_details | text | 65535 |  | Y | 无 | 停机详情 |
| 21 | alarm_details | text | 65535 |  | Y | 无 | 报警详情 |
| 22 | responsible_department | varchar | 100 |  | Y | 无 | 责任部门 |
| 23 | responsible_person | varchar | 50 |  | Y | 无 | 责任人 |
| 24 | downtime_type | varchar | 50 |  | Y | 无 | 停机类型（计划内停机，计划外停机） |
| 25 | abnormal_reason | text | 65535 |  | Y | 无 | 异常原因 |
| 26 | handling_measures | text | 65535 |  | Y | 无 | 处理措施 |
| 27 | create_time | datetime |  |  | N | CURRENT_TIMESTAMP | 创建时间 |
| 28 | update_time | datetime |  |  | N | CURRENT_TIMESTAMP | 更新时间 |
| 29 | create_by | varchar | 64 |  | Y | 无 | 创建人 |
| 30 | update_by | varchar | 64 |  | Y | 无 | 更新人 |
| 31 | responsible_department_id | bigint | 19 | 0 | Y | 无 | 责任部门ID |
| 32 | responsible_person_id | bigint | 19 | 0 | Y | 无 | 责任人ID |
| 33 | cancel | int | 10 | 0 | Y | 0 | 取消标识 |
| 34 | equipment_code | varchar | 255 |  | Y | 无 | 设备编码 |
| 35 | equipment_name | varchar | 255 |  | Y | 无 | 设备名称 |
| 36 | source | int | 10 | 0 | Y | 1 | 来源1 IOT ,  / 2 HUMAN / |
| 37 | accept_order_time | datetime |  |  | Y | 无 | 接收工单时间 |
| 38 | order_generate_time | datetime |  |  | Y | 无 | 工单生成时间 |
| 39 | big_department_code | varchar | 255 |  | Y | 无 | 大部门编码 |
| 40 | big_department_name | varchar | 255 |  | Y | 无 | 大部门名称 |

### oee_loss_type

**业务用途（初步解读）**：用于承载“OEE loss type”相关数据；具体业务含义以字段说明和详细设计流程为准。

**关键字段线索**：id（主键编号）；charge_dept_id（责任部门ID）；charge_character_id（责任人ID）；type（子类型 / 类型1 / 类型2）

| 编号 | 字段名 | 数据类型 | 长度 | 小数位 | 允许空值 | 默认值 | 说明 |
|---|---|---|---|---|---|---|---|
| 1 | id | bigint | 19 | 0 | N | 无 | 主键编号 |
| 2 | name | varchar | 255 |  | Y | 无 | 名称 |
| 3 | picked | int | 10 | 0 | Y | 1 | 挑选标记 / 1是 / 0否 |
| 4 | weight | double | 22 |  | Y | 1 | 权重 / |
| 5 | create_time | datetime |  |  | Y | 无 | 创建时间 |
| 6 | create_by | varchar | 255 |  | Y | 无 | 创建人 |
| 7 | update_time | datetime |  |  | Y | 无 | 修改时间 |
| 8 | update_by | varchar | 255 |  | Y | 无 | 修改人 |
| 9 | is_leaf | int | 10 | 0 | Y | 0 | 是否叶子节点（1表示叶子节点，0表示非叶子节点） |
| 10 | parent_id | bigint | 19 | 0 | Y | 无 | 父节点Id |
| 11 | charge_dept_id | bigint | 19 | 0 | Y | 无 | 责任部门ID |
| 12 | charge_dept_name | varchar | 255 |  | Y | 无 | 责任部门名称 |
| 13 | charge_character_id | bigint | 19 | 0 | Y | 无 | 责任人ID |
| 14 | charge_character_name | varchar | 255 |  | Y | 无 | 责任人名称 |
| 15 | device_type_code | varchar | 255 |  | Y | 无 | 设备类型编码 |
| 16 | device_type_name | varchar | 255 |  | Y | 无 | 设备类型名称 |
| 17 | type | int | 10 | 0 | Y | 1 | 子类型 / 类型1 / 类型2 |

### oee_production_metrics_by_equipment

**业务用途（初步解读）**：用于承载“OEE production metrics by equipment”相关数据；具体业务含义以字段说明和详细设计流程为准。

**关键字段线索**：id（数据ID）

| 编号 | 字段名 | 数据类型 | 长度 | 小数位 | 允许空值 | 默认值 | 说明 |
|---|---|---|---|---|---|---|---|
| 1 | id | bigint | 19 | 0 | N | 无 | 数据ID |
| 2 | date | date |  |  | Y | 无 | 日期 |
| 3 | shift | varchar | 255 |  | Y | 无 | 班次 |
| 4 | start_time | datetime |  |  | Y | 无 | 开始时间 |
| 5 | end_time | datetime |  |  | Y | 无 | 结束时间 |
| 6 | equipment_code | varchar | 255 |  | Y | 无 | 设备编码 |
| 7 | fty | double | 22 |  | Y | 无 | 一次合格率 |
| 8 | first_pass_qty | double | 22 |  | Y | 无 | 一次合格数 |
| 9 | first_defect_qty | double | 22 |  | Y | 无 | 一次不良数 |
| 10 | actual_production | double | 22 |  | Y | 无 | 实际产量 |

### oee_production_metrics_by_factory_instance

**业务用途（初步解读）**：用于承载“OEE production metrics by factory instance”相关数据；具体业务含义以字段说明和详细设计流程为准。

**关键字段线索**：id（数据ID）

| 编号 | 字段名 | 数据类型 | 长度 | 小数位 | 允许空值 | 默认值 | 说明 |
|---|---|---|---|---|---|---|---|
| 1 | id | bigint | 19 | 0 | N | 无 | 数据ID |
| 2 | date | date |  |  | Y | 无 | 日期 |
| 3 | shift | varchar | 255 |  | Y | 无 | 班次 |
| 4 | start_time | datetime |  |  | Y | 无 | 开始时间 |
| 5 | end_time | datetime |  |  | Y | 无 | 结束时间 |
| 6 | fty | double | 22 |  | Y | 无 | 一次合格率 |
| 7 | first_pass_qty | double | 22 |  | Y | 无 | 一次合格数 |
| 8 | first_defect_qty | double | 22 |  | Y | 无 | 一次不良数 |
| 9 | actual_production | double | 22 |  | Y | 无 | 实际产量 |
| 10 | factory_instance_code | varchar | 255 |  | Y | 无 | 企业层级编码 |
| 11 | factory_instance_name | varchar | 255 |  | Y | 无 | 企业层级名称 |
| 12 | factory_instance_full_path_name | varchar | 255 |  | Y | 无 | 企业层级整路径名称 |

### oee_snapshot

**业务用途（初步解读）**：用于承载“OEE snapshot”相关数据；具体业务含义以字段说明和详细设计流程为准。

**关键字段线索**：id（主键ID）

| 编号 | 字段名 | 数据类型 | 长度 | 小数位 | 允许空值 | 默认值 | 说明 |
|---|---|---|---|---|---|---|---|
| 1 | id | bigint | 19 | 0 | N | 无 | 主键ID |
| 2 | factory | varchar | 100 |  | Y | 无 | 工厂编码 |
| 3 | factory_name | varchar | 100 |  | Y | 无 | 工厂名称 |
| 4 | line | varchar | 100 |  | Y | 无 | 线体 |
| 5 | line_name | varchar | 100 |  | Y | 无 | 线体名称 |
| 6 | process | varchar | 100 |  | Y | 无 | 工序 |
| 7 | process_name | varchar | 100 |  | Y | 无 | 工序名称 |
| 8 | space_code | varchar | 255 |  | N | 无 | 空间编码 |
| 9 | space_name | varchar | 255 |  | Y | 无 | 空间名称 |
| 10 | time | varchar | 255 |  | N | 无 | 时间维度值 |
| 11 | scale | varchar | 50 |  | Y | 无 | 时间维度类型（QUARTER，季）（YEAR，年）（WEEK，周）（MONTH，月）（SHIFT，班次） |
| 12 | space_type | varchar | 50 |  | Y | EQUIPMENT | 空间类型（EQUIPMENT，"PROCESS"; "LINE". "FACTORY"; "BASE";） |
| 13 | start_time | datetime |  |  | Y | 无 | 开始时间 |
| 14 | end_time | datetime |  |  | Y | 无 | 结束时间 |
| 15 | snapshot | text | 65535 |  | N | 无 | OEE快照数据JSON |
| 16 | create_time | datetime |  |  | N | CURRENT_TIMESTAMP | 创建时间 |
| 17 | update_time | datetime |  |  | N | CURRENT_TIMESTAMP | 更新时间 |
| 18 | create_by | varchar | 64 |  | Y | 无 | 创建人 |
| 19 | update_by | varchar | 64 |  | Y | 无 | 更新人 |
| 20 | deleted | tinyint | 3 | 0 | N | 0 | 是否删除（1是0否） |
| 21 | archived | int | 10 | 0 | Y | 0 | 是否归档（1是0否） |

### oee_snapshot_audit

**业务用途（初步解读）**：用于承载“OEE snapshot audit”相关数据；具体业务含义以字段说明和详细设计流程为准。

**关键字段线索**：id（主键ID）

| 编号 | 字段名 | 数据类型 | 长度 | 小数位 | 允许空值 | 默认值 | 说明 |
|---|---|---|---|---|---|---|---|
| 1 | id | bigint | 19 | 0 | N | 无 | 主键ID |
| 2 | factory | varchar | 100 |  | Y | 无 | 工厂编码 |
| 3 | factory_name | varchar | 100 |  | Y | 无 | 工厂名称 |
| 4 | line | varchar | 100 |  | Y | 无 | 线体编码 |
| 5 | line_name | varchar | 100 |  | Y | 无 | 线体名称 |
| 6 | process | varchar | 100 |  | Y | 无 | 工序 |
| 7 | process_name | varchar | 100 |  | Y | 无 | 工序名称 |
| 8 | space_code | varchar | 255 |  | N | 无 | 空间编码 |
| 9 | space_name | varchar | 255 |  | Y | 无 | 空间名称 |
| 10 | time | varchar | 255 |  | N | 无 | 时间维度值 |
| 11 | scale | varchar | 50 |  | Y | 无 | 时间维度类型（QUARTER，季）（YEAR，年）（WEEK，周）（MONTH，月）（SHIFT，班次） |
| 12 | space_type | varchar | 50 |  | Y | EQUIPMENT | 空间类型（EQUIPMENT，"PROCESS"; "LINE". "FACTORY"; "BASE";） |
| 13 | start_time | datetime |  |  | Y | 无 | 开始时间 |
| 14 | end_time | datetime |  |  | Y | 无 | 结束时间 |
| 15 | snapshot | text | 65535 |  | N | 无 | OEE快照数据JSON |
| 16 | create_time | datetime |  |  | N | CURRENT_TIMESTAMP | 创建时间 |
| 17 | update_time | datetime |  |  | N | CURRENT_TIMESTAMP | 更新时间 |
| 18 | create_by | varchar | 64 |  | Y | 无 | 创建人 |
| 19 | update_by | varchar | 64 |  | Y | 无 | 更新人 |
| 20 | deleted | tinyint | 3 | 0 | N | 0 | 是否删除（1是0否） |
| 21 | archived | int | 10 | 0 | Y | 0 | 是否归档（1归档 , 0未归档） / |
