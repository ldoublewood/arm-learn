---
category: concept
tags: [dexterity, manipulation, grasping, in-hand-manipulation]
created: 2026-06-28
updated: 2026-06-28
related: [[concepts/tactile-sensing]], [[papers/fabisch-2025-anthropomorphic-hands]]
---

# 灵巧操作（Dexterous Manipulation）

## 定义（Definition）

灵巧操作（Dexterous Manipulation）指机器人末端执行器（手/夹爪）对物体进行精细、多自由度的操控能力，包括抓取（grasping）、掌内操作（in-hand manipulation）、工具使用（tool use）等。灵巧操作的核心是在保持稳定接触的同时改变物体的位姿（位置和姿态），通常需要多指协调、触觉反馈和高级控制策略的配合。

## 关键原理（Key Principles）

- **接触建模**：灵巧操作的基础是手指与物体之间的接触力学。每个接触点可施加法向力和切向力，摩擦力锥（friction cone）决定了抓取的稳定性边界
- **运动学冗余**：多指手拥有比任务需求更多的自由度，这种冗余性提供了操作的灵活性，但也增加了控制难度
- **力封闭与形封闭**：力封闭（force closure）指手指力可抵抗任意方向的外力扰动；形封闭（form closure）指物体的几何形状被手指包围约束。灵巧操作需要在这两种状态间切换
- **指内操作与指间操作**：指内操作（within-finger）通过手指关节运动改变物体位姿；指间操作（between-finger）通过手指间的协调重排实现物体重新定位

## Dollar 操作分类法（Dollar's Manipulation Taxonomy）

Dollar 提出的操作分类法独立于手部形态，将操作技能分为：

**抓取类（Prehensile）：**
- 抓握（Grasp）：手指包裹物体形成稳定抓取
- 掌内操作（In-Hand Manipulation）：在不释放物体的情况下改变其相对手部的位姿

**非抓取类（Non-Prehensile）：**
- 推动（Pushing）：通过手指推动改变物体在支撑面上的位置
- 手势/示意（Gesturing）：手部姿态表达，不涉及物体操控

## 手指数量与灵巧度的关系

根据系统综述研究：
- **2指**：可完成大量任务，配合环境约束（environment constraints）可扩展操作能力
- **3指**：简洁性与灵巧性的最佳折中，支持工具使用和抓取稳定化
- **4指（非仿人）**：两对相对手指可实现6 DoF掌内操作
- **5指及以上**：支持并行多物体操作，但控制复杂度显著增加

关键发现：手指数量与操作技能复杂度之间**无显著统计相关性**——设计良好的简单机构可以达到与复杂仿人手相当的操作能力。

## 与工业机械臂的关系（Relevance to Industrial Robotic Arms）

- 工业场景的末端执行器选型：平行夹爪适合大多数拾放任务；需要灵巧操作时可选择3指夹爪
- 环境约束利用：通过将物体推向桌面/夹具等环境表面，可显著降低对末端执行器复杂度的要求
- 手腕灵活性投资：在手腕增加自由度（俯仰/偏航）比增加手指数量更能提升操作能力
- 触觉传感器集成是工业级灵巧操作的关键瓶颈

## 相关概念（Related Concepts）

- [[concepts/tactile-sensing]] — 触觉感知是实现闭环灵巧操作的前提
- [[concepts/impedance-control]] — 力控策略用于实现稳定抓取和力封闭
- [[concepts/imitation-learning]] — 灵巧操作策略可通过遥操作示教学习
- [[papers/fabisch-2025-anthropomorphic-hands]] — 系统综述：仿人手设计的必要性质疑

## 参考文献（References）

- [Fabisch 2025 - Anthropomorphic Hands Survey](raw/papers/2026-06-28-anthropomorphic-hands-survey.md)
