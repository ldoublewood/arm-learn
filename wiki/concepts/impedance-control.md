---
category: concept
tags: [force-control, dynamics]
created: 2026-06-24
updated: 2026-06-24
related: [[concepts/admittance-control]], [[tools/ros2-control]]
---

# 阻抗控制（Impedance Control）

## 定义（Definition）

阻抗控制（impedance control）是工业机械臂动态控制的一种方法，由 Neville Hogan 于 1985 年提出。与传统的精确位置控制不同，阻抗控制调节的是机械臂运动与环境作用力之间的**动态关系**——让机器人像一个质量-弹簧-阻尼系统一样对外力做出响应，而非僵硬地维持预定位置。

## 核心原理（Key Principles）

- **质量-弹簧-阻尼模型**：目标阻抗由惯性矩阵 M、阻尼矩阵 B、刚度矩阵 K 三个参数共同定义
- **力-运动关系**：阻抗控制接受力输入，产生运动输出——机器人是"机械阻抗"
- **可调顺应性**：通过调节 M、B、K 三个参数，可以在"完全刚性"（高刚度）和"完全柔顺"（低刚度）之间自由切换

## 数学模型（Mathematical Foundation）

目标阻抗方程：

$$M(\ddot{x} - \ddot{x}_d) + B(\dot{x} - \dot{x}_d) + K(x - x_d) = F_{ext}$$

其中：
- $M$ — 期望惯性矩阵（desired inertia matrix），影响加速度响应
- $B$ — 期望阻尼矩阵（desired damping matrix），影响速度响应
- $K$ — 期望刚度矩阵（desired stiffness matrix），影响位置响应
- $x$ — 实际位置，$x_d$ — 期望位置
- $F_{ext}$ — 外部作用力

### 参数调谐直觉

- **高刚度 K**：机器人"硬"，外力推不动 → 接近纯位置控制
- **低刚度 K**：机器人"软"，轻易被外力推动 → 接近纯力控制
- **高阻尼 B**：运动平稳，但响应慢
- **低阻尼 B**：响应快，但可能振荡

## 关键应用（Key Applications）

1. **装配任务（Assembly tasks）** — 机器人插入零件时可以顺应，防止卡死和损坏
2. **抛光打磨（Polishing and grinding）** — 跟随曲面时保持恒定的接触力
3. **人机协作（Human-robot interaction）** — 使机器人在人类靠近时表现出安全、柔顺的行为
4. **未知环境（Unknown environments）** — 机器人可以适应不确定的接触条件

## 与导纳控制的关系（Relation to Admittance Control）

阻抗控制与[[concepts/admittance-control|导纳控制]]（admittance control）互为对偶：

| 特性 | 阻抗控制 | 导纳控制 |
|------|----------|----------|
| 因果关系 | 力输入 → 运动输出 | 运动输入 → 力输出 |
| 适用机器人 | 轻量、反向可驱动机器人 | 重型、非反向可驱动工业臂 |
| 实现方式 | 直接力矩控制 | 位置控制内环 + 力控制外环 |

## 参考文献（References）

- [阻抗控制入门介绍](raw/articles/2026-06-24-impedance-control-intro.md)
