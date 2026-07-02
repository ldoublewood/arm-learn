---
category: concept
tags: [VLA, imitation-learning, embodied-AI, policy-learning]
created: 2026-06-27
updated: 2026-06-27
related: [[imitation-learning]], [[../tools/lerobot]]
---

# VLA 视觉-语言-动作模型（Vision-Language-Action Model）

## 定义（Definition）

VLA（Vision-Language-Action）是一类将视觉感知、语言理解和动作生成融为一体的端到端模型架构。VLA 模型直接以图像（vision）和自然语言指令（language）作为输入，输出机器人动作序列（action），实现从感知到控制的完整闭环。VLA 是具身智能（Embodied AI）领域的核心技术路线之一。

## 关键原理（Key Principles）

- **多模态输入融合**：同时处理相机图像（RGB/深度）和文本指令，通过共享特征空间实现跨模态理解
- **端到端学习**：从原始传感器数据直接映射到关节角度/末端位姿，无需手工设计运动学/动力学模型
- **模仿学习驱动**：通过人类遥操作示范（demonstration）采集数据，行为克隆（Behavioral Cloning）训练策略
- **Action Chunking**：一次预测未来多个时间步的动作序列（chunk），提升动作的时序一致性和鲁棒性

## 主流架构

### ACT（Action Chunking Transformer）
- 轻量级 VLA 策略，可在边缘设备（如 Raspberry Pi）上实时推理
- 基于 Transformer 的 encoder-decoder 架构
- 将图像特征和关节状态编码后，解码输出未来 N 步的动作序列

### SmolVLA
- 更强大的 VLA 模型变体
- 需要 GPU 加速推理
- 支持更复杂的多任务场景

### Pi0 / Pi0.5
- 前沿 VLA 模型（Physical Intelligence 提出）
- 结合大规模预训练和机器人微调
- 需要独立 GPU 服务器运行推理

## 训练流程

1. **数据采集（Data Collection）**：通过遥操作（leader arm 或 VR）收集人类示范数据集，包含同步的相机图像和关节状态
2. **策略训练（Policy Training）**：使用 LeRobot 等框架训练模仿学习策略
3. **模型部署（Deployment）**：轻量策略本地运行，重量策略通过异步推理（async inference）客户端-服务器模式部署

## 与工业机械臂的关系（Relevance to Industrial Robotic Arms）

VLA 模型为工业机械臂提供了一种新的编程范式——通过人类示范而非手工编程来定义任务。在结构化程度较低的工业场景（如物流分拣、柔性装配）中，VLA 可显著降低部署成本。当前局限在于：
- 精度尚不及传统运动规划方法
- 需要大量示范数据
- 泛化能力受限于训练场景分布

## 相关概念（Related Concepts）

- [[imitation-learning]] — VLA 的核心训练方法是模仿学习
- [[../tools/lerobot]] — HuggingFace 的机器人学习框架，VLA 训练的主要工具
- [[impedance-control]] — 传统控制方法与学习方法的对照

## 参考文献（References）

- [VLA Training for XLeRobot](../../raw/docs/2026-06-27-vla-xlerobot.md)
