## 🎓 教学案例模板：学生选课管理系统（Student Course Management System, SCMS）

---

### 🧭 一、项目简介
**项目名称：** 学生选课管理系统（SCMS）  
**项目类型：** 教学示例 / 瀑布模型实践项目  
**开发模式：** 瀑布开发模型（Waterfall Model）  
**教学阶段涵盖：** 基本设计（概要设计）+ 详细设计  

**项目目标：**
- 模拟高校选课业务流程，帮助学习者掌握从需求分析到系统设计的全过程；
- 实践概要设计与详细设计的文档编写与建模方法；
- 提高系统分析与设计能力。

---

### 📘 二、项目需求说明书（SRS 摘要）

#### 1. 功能需求
| 模块 | 功能描述 |
|------|------------|
| 用户管理 | 提供学生、教师、管理员注册、登录及权限控制功能 |
| 课程管理 | 管理课程信息（新增、修改、删除、查询） |
| 选课模块 | 学生进行选课、退课操作；防止重复选课与人数超限 |
| 成绩管理 | 教师录入、修改成绩；学生可查询成绩 |
| 报表模块 | 管理员导出选课及成绩统计报表 |

#### 2. 非功能需求
- **性能要求：** 系统应支持 1000 名学生并发选课；
- **安全要求：** 所有用户操作需登录认证；
- **可维护性：** 模块间耦合度低、接口定义规范；
- **可靠性：** 选课、退课操作需事务保护。

#### 3. 运行环境
- 前端：Web（HTML5 + Vue / React）  
- 后端：Java / Spring Boot 或 Python / Django  
- 数据库：MySQL  
- 运行平台：Windows / Linux  

---

### 🏗️ 三、概要设计说明书（SDS 模板）

#### 1. 系统结构图
以三层架构为基础：
```
表示层（UI） → 业务逻辑层（Service） → 数据层（DAO / Database）
```

#### 2. 模块划分
| 模块名称 | 职责说明 | 输入 | 输出 |
|-----------|------------|------|------|
| 用户管理模块 | 处理注册、登录、权限验证 | 用户数据 | 登录状态、权限标识 |
| 课程管理模块 | 管理课程信息 | 课程数据 | 课程列表 |
| 选课模块 | 学生选课、退课操作 | 学生/课程编号 | 操作结果 |
| 成绩模块 | 教师录入成绩 | 成绩数据 | 成绩单 |
| 报表模块 | 生成统计报表 | 查询条件 | 报表数据 |

#### 3. 模块关系图
（建议使用 PlantUML / draw.io 绘制）

#### 4. 数据库概要设计（ER 图）
**主要实体：**
- `User(UserID, Name, Role, Password)`
- `Course(CourseID, CourseName, Credit, TeacherID)`
- `Enrollment(EnrollID, StudentID, CourseID, Grade)`

#### 5. 技术选型说明
| 类别 | 选型 | 说明 |
|------|------|------|
| 语言 | Java / Python | 兼容主流教学环境 |
| 数据库 | MySQL | 支持事务与外键约束 |
| 架构 | MVC | 模块职责清晰 |
| 工具 | draw.io / PlantUML / MySQL Workbench | 适用于教学与建模 |

#### 6. 概要设计检验指标
- ✅ 模块划分合理、依赖关系明确；
- ✅ 系统结构图完整、层次清晰；
- ✅ ER 图反映主要业务逻辑。

---

### ⚙️ 四、详细设计说明书（DDS 模板）

#### 1. 模块分解
以“选课模块”为例：

**模块名称：** 选课模块（Enrollment Module）  
**主要类：**
- `EnrollmentController`（负责接收选课请求）
- `EnrollmentService`（选课业务逻辑）
- `EnrollmentDAO`（数据库访问）

#### 2. 类图示例
```
+-------------------+
| EnrollmentService |
+-------------------+
| +enroll(student, course) |
| +drop(student, course)   |
+-------------------+
```

#### 3. 顺序图（选课流程）
```
Student -> UI: 提交选课请求
UI -> Controller: 调用 enroll()
Controller -> Service: 验证选课条件
Service -> DAO: 写入选课记录
DAO -> DB: 提交事务
Service -> Controller: 返回选课成功
Controller -> UI: 显示成功信息
```

#### 4. 数据库详细设计
| 表名 | 字段 | 类型 | 约束 |
|------|------|------|------|
| User | UserID | INT | PK |
| Course | CourseID | INT | PK |
| Enrollment | EnrollID | INT | PK |
| | StudentID | INT | FK(UserID) |
| | CourseID | INT | FK(CourseID) |
| | Grade | DECIMAL(3,1) | 可空 |

#### 5. 异常与日志设计
- **异常：** 当课程人数已满或重复选课时抛出 `EnrollmentException`；
- **日志：** 所有选课操作记录写入 `EnrollLog` 表。

#### 6. 伪代码示例
```pseudo
function enroll(studentID, courseID):
    if not isLoggedIn(studentID):
        raise AuthException
    if isCourseFull(courseID):
        raise EnrollmentException
    if alreadyEnrolled(studentID, courseID):
        raise DuplicateEnrollment
    saveEnrollment(studentID, courseID)
    log("Student %s enrolled in %s" % (studentID, courseID))
    return Success
```

#### 7. 详细设计检验指标
- ✅ 类图、顺序图、伪代码齐全；
- ✅ 数据表字段定义准确；
- ✅ 异常与日志设计覆盖主要流程。

---

### 📋 五、评审与验收
| 检验维度 | 评价标准 |
|------------|-----------|
| 设计一致性 | 概要与详细设计保持一致；模块与类一一对应 |
| 完整性 | 所有主要功能均有设计描述 |
| 可追踪性 | 各设计元素可追溯至需求说明 |
| 可实现性 | 设计逻辑清晰，可直接指导编码 |

---

### 🧾 六、教学成果清单
1. 《需求规格说明书》（SRS）  
2. 《概要设计说明书》（SDS）  
3. 《详细设计说明书》（DDS）  
4. 系统架构图、模块图、ER 图、类图、顺序图  
5. 伪代码与设计评审报告  

---

### 🧠 七、可扩展任务（供进阶教学使用）
- 添加**选课冲突检测算法**；
- 集成**课程容量自动调整**逻辑；
- 扩展为 RESTful API，并使用 Swagger 生成接口文档；
- 增加**选课统计可视化界面**（使用 ECharts / Chart.js）。

