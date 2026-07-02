---
category: concept
tags: [imitation-learning, behavioral-cloning, demonstration, policy-learning]
created: 2026-06-27
updated: 2026-06-27
related: [[vla-vision-language-action]], [[../tools/lerobot]]
---

# 模仿学习（Imitation Learning）

## 定义（Definition）

模仿学习（Imitation Learning，IL）是一种从专家示范（demonstration）中学习策略的机器学习方法。在机器人领域，模仿学习通过记录人类操作机械臂的轨迹数据（关节角度、末端位姿、相机图像），训练神经网络策略直接输出控制指令，使机器人能够复现人类演示的任务。模仿学习是实现具身智能（Embodied AI）的核心技术路径之一。

## 关键原理（Key Principles）

- **行为克隆（Behavioral Cloning, BC）**：将专家示范视为监督学习问题，直接学习状态到动作的映射。训练目标为最小化预测动作与专家动作的差异
- **分布偏移（Distribution Shift）**：BC 的主要挑战——策略执行时的误差累积导致机器人进入训练分布之外的状态，引发级联失败
- **Action Chunking**：一次预测多步动作序列（而非单步），减少累积误差，提升时序一致性
- **数据集聚合（DAgger）**：通过迭代收集策略执行中的状态并请求专家标注，逐步修正分布偏移

## 数据采集方式

### 遥操作示教（Teleoperation）
- **Leader-Follower 架构**：人类操作 leader arm（轻量、无动力或反向驱动），follower arm 同步记录关节状态
- **VR 遥操作**：通过 VR 手柄控制机械臂，提供更直观的操作体验
- **拖动示教（Kinesthetic Teaching）**：直接手拉机械臂末端执行任务，记录轨迹

### 数据质量要求
- 场景一致性：数据采集与部署环境应保持相同的相机位置、光照、背景
- 避免冗余帧：任务完成后立即结束录制，避免记录静止状态
- 帧率稳定：监控带宽和 CPU 使用率，避免掉帧

## 训练框架

- [[../tools/lerobot|LeRobot]]：HuggingFace 的机器人学习框架，支持 ACT、Diffusion Policy 等主流算法
- **RoboMimic**：Stanford 的模仿学习基准框架
- **RoboTwin**：双臂模仿学习框架

## 与工业机械臂的关系（Relevance to Industrial Robotic Arms）

模仿学习为工业场景中难以精确建模的任务提供了替代方案：
- **优势**：无需精确的运动学/动力学标定，对非结构化环境更具适应性
- **局限**：精度不及传统轨迹规划，泛化性受限于训练数据分布，安全性验证困难
- **适用场景**：物流分拣、柔性装配、表面处理（擦拭、打磨）等

## 相关概念（Related Concepts）

- [[vla-vision-language-action]] — 结合视觉和语言的模仿学习扩展
- [[impedance-control]] — 传统力控方法与学习方法的互补
- [[../tools/ros2-control]] — 传统控制框架，可与学习策略混合使用

## 参考文献（References）

- [VLA Training for XLeRobot](../../raw/docs/2026-06-27-vla-xlerobot.md)
