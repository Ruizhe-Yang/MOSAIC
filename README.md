<p align="center">
  <img src="assets/brand/MOSAIC_logo.svg" alt="MOSAIC — Modelica-Oriented System Architecture, Interfaces and Contracts" width="780">
</p>

<h1 align="center">MOSAIC</h1>
<p align="center"><strong>Modelica-Oriented System Architecture, Interfaces and Contracts</strong><br>
面向 Modelica 的总体级系统架构、接口与契约建模规范</p>
<p align="center"><em>Model the Whole as MOSAIC.</em></p>

<p align="center">
  <a href="./MOSAIC_v0.8_Modelica_Modeling_Standard.html">📘 中文完整规范 · v0.8</a>
  &nbsp;·&nbsp;
  <a href="https://github.com/Ruizhe-Yang/modelica-system-level-simulation-skill">🛠️ MOSAIC-skill · AI 辅助实施</a>
</p>

**MOSAIC** 面向复杂系统的 Modelica 总体级建模与多物理场仿真，提供一套能够落实到具体模型、接口、参数、图形和验证工作的工程规范。它从真实系统的组成和工作关系出发，统一约定**模型角色、结构与行为分工、接口契约、配置来源、模型可视化以及仿真证据**，帮助工程师建立可理解、可配置、可扩展、可维护的系统模型。

> **English overview:** MOSAIC is a practical modeling methodology and engineering specification for **system-level, multi-physics modeling with Modelica**. It defines how to organize system architecture, assign behavior to components, manage interfaces and configuration, and maintain traceable simulation evidence. The companion [MOSAIC-skill](https://github.com/Ruizhe-Yang/modelica-system-level-simulation-skill) helps AI coding agents apply these conventions to real projects. MOSAIC is **not** a simulation solver or an additional Modelica runtime library.

## 从哪里开始？

| 你的目标 | 推荐入口 |
|---|---|
| 了解 MOSAIC 的完整规则与设计思想 | **[阅读 MOSAIC v0.8 中文建模规范（HTML）](./MOSAIC_v0.8_Modelica_Modeling_Standard.html)** |
| 在已有 Modelica 工程中检查架构、接口、文档或图形 | **[使用 MOSAIC-skill](https://github.com/Ruizhe-Yang/modelica-system-level-simulation-skill)** 的审查与限定维护模式 |
| 新建总体级仿真项目 | 先确定系统边界、模型角色、配置和验收指标，再参照规范建模；可选用 MOSAIC-skill 辅助实施 |
| 了解规范和 AI 技能的区别 | 阅读下方“**MOSAIC 与 MOSAIC-skill**” |

本仓库目前以**中文 HTML 规范**为主要交付物。打开上方文件链接后，可在 GitHub 页面下载原始 HTML，再用浏览器本地阅读；规范包含条文、分类说明与相关参考内容。

## 解决什么工程问题？

大型 Modelica 项目经常面临系统层级与物理计算混杂、接口语义不清、参数来源分散、画布与实际连接不一致，以及模型迭代后难以复用既有工作等问题。MOSAIC 把这些问题转化为可以逐项检查的建模约定：

- **架构清晰：** 用真实系统、分系统、装配和行为单元组织模型，让 Diagram 反映实际实例和连接。
- **职责明确：** 区分只负责组织与连接的白箱，以及承担物理方程、控制算法和状态的行为单元。
- **接口可信：** 优先复用 Modelica Standard Library（MSL）的接口语义，明确能量、物质、机械、热、电和信号交互。
- **配置同源：** 明确参数、曲线、单位和初态的权威来源；允许从 Excel 等设计表离线生成最终 Modelica 源码，运行时不依赖办公软件。
- **图形可用：** 使 Icon、Diagram、Placement 与真实端口、`connect` 对应，区分 MSL 原生接口线色与自定义接口线色。
- **验证有据：** 区分静态审查、编译、初始化、完整任务仿真、结果校核和模型保真度评估，不以其中一项代替全部。

## 核心建模框架：五种模型角色

MOSAIC 使用五种**职责角色**组织可执行系统模型。它们是建模概念，**不要求在实际类名中添加 TB/SB/AB/BU/LU 前缀**。

| 角色 | 定位 | 主要责任 |
|---|---|---|
| **TB — Top-level Box** | 顶层盒 · 白箱 | 定义完整仿真入口、实验构型、系统/环境实例及静态连接 |
| **SB — System Box** | 系统盒 · 白箱 | 组织真实系统或分系统的集成边界、公开接口及内部组成 |
| **AB — Assembly Box** | 装配盒 · 白箱 | 在末级组合 BU/LU，建立必要的静态连接与装配边界 |
| **BU — Behavior Unit** | 行为单元 · 黑箱 | 实现内聚的物理方程、控制算法、状态与初始化 |
| **LU — Library Unit** | 库复用单元 · 黑箱 | 复用 MSL 原生组件或未改变行为的静态/展示别名 |

**关键约定：TB、SB、AB 的本层只承担声明、静态配置和连接；本构、控制与状态演化由明确的 BU/LU 承担。** 具体继承、修饰、初始化、嵌套和允许的连接模板，以完整规范中的角色清单为准。

## v0.8 规范包含什么？

当前版本提供 **M01—M36 共 36 项主条文**，分为 **26 项必须（R）、9 项建议（S）和 1 项参考（F）**，另有专题参考与实施说明。主要覆盖：

| 主题 | 规范重点 |
|---|---|
| 系统架构与模型角色 | 真实组成、统一执行网络、五类角色、白箱与行为边界 |
| 多物理场接口与状态 | 连接器语义、MSL 复用、信号身份、单位、状态拥有者 |
| 参数配置与工程结构 | 设计配置、曲线数据、离线生成、依赖与版本一致性 |
| 图形、文档与品牌 | 原生 Diagram、功能 Icon、连线颜色、类说明与文档规则 |
| 仿真验证与模型演进 | 编译运行、证据边界、结果诊断、变更保护与工程交付 |

工程默认基于项目自有 Modelica 源码和 **MSL 4.0.0**；对于已有工程，遵守其已冻结的有效依赖版本，不因阅读本规范而自动升级。规范适用于航天器、航空器、燃气轮机及其他需要总体级多物理场建模的对象，但不预设所有行业采用相同的系统划分、参数或物理模型。

## MOSAIC 与 MOSAIC-skill

两者属于**同一方法体系的两个层次**：一个定义工程规则，一个辅助执行工程规则。

```mermaid
flowchart LR
    A["MOSAIC 规范<br/>建模原则 · M01–M36 · 模型角色"] --> B["MOSAIC-skill<br/>AI 工作流 · 参考资料 · 静态辅助工具"]
    A --> C["实际 Modelica 工程<br/>架构 · 接口 · 配置 · 行为"]
    B --> C
    C --> D["Modelica 工具环境<br/>编译 · 仿真 · 验证"]
```

| 项目 | [MOSAIC（本仓库）](https://github.com/Ruizhe-Yang/MOSAIC) | [MOSAIC-skill](https://github.com/Ruizhe-Yang/modelica-system-level-simulation-skill) |
|---|---|---|
| 定位 | 总体建模方法及中文规范 | 面向 AI 编程助手的规范实施技能 |
| 核心内容 | 完整 HTML 条文、角色与接口要求、图形和文档约定 | `SKILL.md`、按任务加载的参考资料、检查脚本、示例与测试 |
| 主要使用者 | 系统建模师、总体设计师、研究人员 | 使用 Codex 或兼容 Agent Skills 宿主开展 Modelica 工程工作的人员 |
| 是否负责数值求解 | 否 | 否；需要已安装的实际 Modelica 工具和明确的执行任务 |

**可以只用 MOSAIC 规范人工建模；使用 MOSAIC-skill 时，则应将本仓库的同版本规范作为方法依据。** Skill 不会自动替代工程师的设计判断，也不保证只靠静态检查即可获得正确的物理仿真结果。

## 推荐的工程工作流

1. **定义任务：** 确认总体模型用途、真实系统边界、运行场景、关键指标和约束条件。
2. **组织结构：** 分配 TB/SB/AB/BU/LU 角色，先确定真实组成和职责，再确定图形布局。
3. **建立接口：** 优先复用合适的 MSL 接口，明确自定义接口、单位、信号和状态归属。
4. **准备配置：** 管理设计表与曲线的来源，生成可独立加载的 Modelica 工程及确定的生效参数。
5. **形成闭环：** 在真实 Modelica 环境编译、初始化、仿真，检查原始结果、指标和必要的独立证据。
6. **受控演进：** 区分行为优化与纯文档/图形维护，保护已认可的运行基线，记录变更和剩余限制。

## 仓库内容与适用边界

```text
MOSAIC/
├── README.md
├── MOSAIC_v0.8_Modelica_Modeling_Standard.html  # 中文完整建模规范
└── assets/brand/
    ├── MOSAIC_logo.svg                       # 总品牌 LOGO
    └── MOSAIC_symbol.svg                     # 品牌符号
```

本仓库目前**不分发独立的 Modelica 运行库、求解器或完整案例仿真工程**。MOSAIC-skill 仓库提供一个 12UCubeSat 工程的**方法使用说明**，但也不随仓库附带该项目的完整模型及运行数据。将规范应用于实际工程时，物理实现、模型保真度、工具兼容性和验证结论需要分别确认。

欢迎通过 GitHub Issues 交流条文理解、实际建模经验、接口设计与规则改进建议。

---

<p align="center"><strong>Model the Whole as MOSAIC.</strong><br><sub>Architecture · Interfaces · Contracts · Executable Modelica Systems</sub></p>
