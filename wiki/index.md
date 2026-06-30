---
category: index
updated: 2026-06-28
---

# arm-learn 知识索引（Knowledge Index）

工业机械臂（Industrial Robotic Arms）知识库。

## 概念（Concepts）

- [[concepts/impedance-control]] — 阻抗控制：通过调节力与运动的动态关系控制机械臂
- [[concepts/admittance-control]] — 导纳控制：阻抗控制的对偶方法，适用于重型工业臂
- [[concepts/imitation-learning]] — 模仿学习：从人类示范中学习机器人控制策略
- [[concepts/vla-vision-language-action]] — VLA 视觉-语言-动作模型：端到端感知到控制的具身智能方法
- [[concepts/dexterous-manipulation]] — 灵巧操作：多指协调、触觉反馈、精细物体操控
- [[concepts/tactile-sensing]] — 触觉感知：机器人触觉传感器的原理、技术与应用

## 论文（Papers）

- [[papers/fabisch-2025-anthropomorphic-hands]] — 系统性综述：机器人是否真的需要仿人手？125篇论文分析

## 工具（Tools）

- [[tools/ros2-control]] — ROS 2 实时控制框架，支持多种控制模式和硬件抽象
- [[tools/lerobot]] — HuggingFace 机器人学习框架，支持模仿学习和 VLA 策略训练

## 资源与平台（Resources & Platforms）

- [[open-source-arm-projects]] — 开源机械臂项目汇总：reBot-DevArm、OpenArm、Panthera-HT、EL-A3、牧卫 Mockway 五大项目的全面对比

## 主题地图（Topic Map）

### 开源平台与生态
- [[open-source-arm-projects]]

### 力控与顺应控制（Force Control & Compliance）
- [[concepts/impedance-control]]
- [[concepts/admittance-control]]

### 抓取与灵巧操作（Grasping & Dexterous Manipulation）
- [[concepts/dexterous-manipulation]]
- [[concepts/tactile-sensing]]
- [[papers/fabisch-2025-anthropomorphic-hands]]

### 模仿学习与具身智能（Imitation Learning & Embodied AI）
- [[concepts/imitation-learning]]
- [[concepts/vla-vision-language-action]]
- [[tools/lerobot]]

### ROS/ROS2 集成
- [[tools/ros2-control]]
