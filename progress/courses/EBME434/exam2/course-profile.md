# EBME 434 · Exam 2 课程档案

建档：2026-10-21（America/New_York）· 更新：2026-10-21（2026-10-21-ebme434-diag01）

## 评分与考试规则（Syllabus，已读）

- Homework 25% · Midterms 60%（三次，默认各 20%；syllabus 未写 drop lowest / curve / 权重差异 / 字母线）· Paper critique 10% · Participation 5%
- 考试：in-class（11:30–12:20，约 50 min）、closed notes、禁用任何技术；"Some exam problems will follow directly from the homework or in-class problems."
- 教材：无，lecture notes 是主要资源

## 考试信息

| 项 | 内容 | 状态 |
|---|---|---|
| Exam 2 | 2026-11-04（周三）课堂时段，closed notes | 已确认（syllabus） |
| Exam 1 | 2026-09-30，**66/100**（Canvas 截图确认）。班级 mean 73.8、median 80.5、20 名学生 | 已确认（教授公告 10/21） |
| Exam 1 补救 | **<70 必须口试**：30 min，白板解 1–2 题（"from the exam, or similar"），可拿回丢分的 1/3（最高到 ≈77.3）。时间：**10/26 那周**，Wickenden 428，用教授链接预约 | 教授公告 10/21；**用户尚未预约** |
| 看卷子 | 教授不发回卷子；10/21 课末 15 min 可看（用户未去），或另约办公室看 | 用户选定"之后自己去找她"，**尚未约** |
| Exam 3 | 2026-12-02 | 已确认 |

## 来源表

| Source ID | 标题 | 路径 | 已读 | 用途 |
|---|---|---|---|---|
| S1 | Tentative Course Schedule | 对话粘贴 | 是 | 日期 |
| S2 | EBME 434 Syllabus Fall 2026.pdf | `Course Information/` | 是（2026-10-21） | 评分规则、考试形式、课表 |
| S3 | Sept 23 postlecture – Numerical Methods & Stiffness | `Professor Class Notes/` | 是 | Exam 1/2 之间：Forward/Backward Euler、Δt < 2/时间常数、stiffness |
| S4 | Sept 28 postlecture – Intro to PDE Modeling & Diffusion | 同上 | 是 | PDE 分类、控制体推导、IC/BC（Dirichlet/Neumann） |
| S5 | Oct 5 postlecture – Diffusion Example 1 (patch on skin) | 同上 | 是 | 单位、Robin BC（蒸发） |
| S6 | October 7 postlecture – Radial Diffusion | 同上 | 是 | 柱/球坐标扩散、Krogh 稳态积分两次 |
| S7 | Oct 12 postlecture – One more thing about Diffusion | 同上 | 是 | t_diff = L²/D、ℓ_diff = √(Dt)、无量纲化 τ = Dt/L² |
| S8 | Oct 14 postlecture – Method of Lines | 同上 | 是 | 有限差分、MoL、边界节点处理 |
| S9 | Oct 14 postlecture – Membrane Potentials & Equivalent Circuits | 同上 | 是 | Nernst、GHK、等效电路（只到图） |
| S10 | HW3（due 10/30） | `HW/EBME 434 2026 Homework 3-1.pdf` | 是 | Q1 特征尺度/无量纲；Q2 球壳稳态扩散-反应；Q3 MoL + 代码 |
| S11 | 用户项目笔记（课程地图、MM、Feedback、Equilibrium、单房室） | claude.ai 项目 docs | 是 | Exam 1 范围与例题 |

**用户自己的笔记（YC Class Notes）只到 9/21**；9/23 之后无个人笔记（用户尚未说明原因）。

## 实际授课顺序（与 syllabus 不同，以讲义文件为准）

| 日期 | 实际讲的 | syllabus 写的 |
|---|---|---|
| 9/21 | Equilibrium & Stability；Feedback Loops | Stability, Least Squares |
| 9/23 | **Numerical Methods & Stiffness** | Least Squares |
| 9/28 | **Intro to PDE & Diffusion** | MLE |
| 9/30 | Exam 1 | Exam 1 |
| 10/5, 10/7 | Diffusion example；Radial diffusion | Diffusion/PDE |
| 10/12, 10/14 | Characteristic scales/nondim；MoL；Membrane potentials | Solutions of PDEs, Cable 1 |
| 10/21 | Cable theory 2（用户未去，等录像/讲义） | Cable 2 |
| 10/26, 10/28 | HH（预计） | HH |
| 11/2 | Deconvolution（预计） | Deconvolution |

→ **Least Squares 和 MLE 从未讲过**；原档案中 T5b/T6 的推断作废。

## Exam 2 范围表

| Topic ID | 主题 | 判定 | 依据 |
|---|---|---|---|
| T5b | 数值求解器与 stiffness（Euler、Δt 上限、ode15s） | **in scope / 边界**（9/23 讲，Exam 1 是否已考未知） | S3 |
| T7 | 扩散方程推导、IC/BC、单位、特征尺度、无量纲化、径向扩散、稳态积分 | **in scope** | S4–S7, S10 |
| T8 | MoL 离散与边界处理 | **in scope** | S8, S10 Q3 |
| T8b | Nernst / GHK / 等效电路 | **in scope** | S9 |
| T9 | Cable theory 2 | in scope（材料待补：10/21 讲义/录像） | — |
| T10 | HH model | in scope（材料待补：10/26, 10/28） | — |
| T11a | Deconvolution（11/2） | **unconfirmed** | 考前两天；Exam 1 同样位置的 9/28 PDE 是否考过未知 |
| T1–T5 | Exam 1 内容 | foundation；口试直接考 | S11 |

## 待解决

1. 用户约口试 + 约看卷子（10/26 那周）
2. Exam 1 逐题错因（看卷后）
3. 补 10/21 cable 2 讲义/录像；10/26–28 HH
4. 向教授确认：Exam 2 是否含 deconvolution；Exam 1 是否 curve/drop（syllabus 无）
