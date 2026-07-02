---
category: concept
tags: [tactile-sensing, haptic-perception, sensors, grasping]
created: 2026-06-28
updated: 2026-06-28
related: [[dexterous-manipulation]], [[../papers/fabisch-2025-anthropomorphic-hands]]
---

# 触觉感知（Tactile Sensing）

## 定义（Definition）

触觉感知（Tactile Sensing）是机器人通过触觉传感器获取接触信息（位置、力、振动、温度、纹理）的能力，是实现灵巧操作（dexterous manipulation）的关键使能技术。触觉感知使机器人能够检测接触状态、感知物体属性、检测滑移并调节抓取力，从而在非结构化环境中安全、可靠地操作物体。

## 关键原理（Key Principles）

### 人体触觉感受器模型

人手有4类主要机械感受器（mechanoreceptors），为机器人触觉传感器设计提供仿生参考：

| 感受器 | 类型 | 功能 | 频率范围 |
|--------|------|------|----------|
| Merkel 细胞（SA I） | 慢适应 | 纹理感知、形状检测，空间分辨率约0.5mm | 0.4–3 Hz |
| Meissner 小体（FA I） | 快适应 | 运动检测、抓取控制，空间分辨率3–4mm | 3–40 Hz |
| Ruffini 小体（SA II） | 慢适应 | 皮肤拉伸、稳定抓取、切向力 | 100–500+ Hz |
| Pacinian 小体（FA II） | 快适应 | 高频振动、工具使用 | 40–500+ Hz |

### 人工触觉传感技术

| 传感原理 | 优点 | 缺点 | 代表产品 |
|----------|------|------|----------|
| **电容式（Capacitive）** | 高灵敏度、低功耗 | 易受电磁干扰 | — |
| **压阻式（Piezoresistive）** | 结构简单、成本低 | 滞后大、温度敏感 | — |
| **压电式（Piezoelectric）** | 高频响应好 | 无法测量静态力 | — |
| **光学式（Optical）** | 高分辨率、可观测几何形变 | 体积较大 | GelSight Mini, DIGIT |
| **磁式（Magnetic）** | 可测3D力矢量 | 易受磁干扰 | uSkin (Xela Robotics) |

### 商用触觉传感器

- **Seed Robotics FTS**：低成本、高分辨率（1mN–30N），温度补偿
- **Xela Robotics uSkin**：磁式3D力矢量传感器，约1.6 tactel/cm²
- **GelSight Mini / DIGIT**：光学式，可捕捉精细几何纹理
- **Contactile PapillArray**：光学式，可测3D偏转/力/振动，推断摩擦和滑移

## 触觉感知在操作中的作用

### 抓取力控制
触觉反馈提供接触力信息，使抓取力刚好超过滑移阈值。无触觉反馈时，内部模型迅速过时，抓取控制性能显著下降。

### 滑移检测（Slip Detection）
检测接触状态的微小变化，及时调整抓取力防止物体脱落。切向力（shear force）信息对滑移检测至关重要。

### 触觉伺服（Tactile Servoing）
以触觉信号为反馈驱动手指运动，实现更安全的环境探索和实时几何特征跟踪。

### 物体属性感知
通过探索性程序（Exploratory Procedures, EPs）判断物体的纹理、硬度、温度、重量、全局形状等。

## 当前局限与挑战

- **传感器集成不足**：大多数研究仅使用1种传感器，多模态触觉融合仍不成熟
- **耐用性与可靠性**：机械鲁棒性、灵敏度一致性、电磁集成和可更换性仍需提升
- **信号处理**：原始触觉数据需要后处理才能用于控制，计算延迟是瓶颈
- **柔性/可拉伸/大面积覆盖**是发展方向
- **工业级触觉传感器成本仍然较高**

## 与工业机械臂的关系（Relevance to Industrial Robotic Arms）

- 精密装配（检测配合状态）、表面处理（控制接触力）、物流分拣（检测滑移）
- 当前工业机械臂大多依赖视觉+位置控制，触觉感知的缺失限制了非结构化场景应用
- 触觉感知是实现从"硬自动化"到"柔性自动化"转型的关键技术

## 相关概念（Related Concepts）

- [[dexterous-manipulation]] — 触觉感知是灵巧操作的基础使能技术
- [[impedance-control]] — 力控与触觉反馈互补，实现柔顺操作
- [[../papers/fabisch-2025-anthropomorphic-hands]] — 系统综述中详细分析了人手与机械手的感知能力对比

## 参考文献（References）

- [Fabisch 2025 - Anthropomorphic Hands Survey](../../raw/papers/2026-06-28-anthropomorphic-hands-survey.md)
