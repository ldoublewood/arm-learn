---
category: concept
tags: [force-control, dynamics]
created: 2026-06-24
updated: 2026-06-24
related: [[concepts/impedance-control]]
---

# 导纳控制（Admittance Control）

## 定义（Definition）

导纳控制（admittance control）是[[concepts/impedance-control|阻抗控制]]（impedance control）的对偶方法。在导纳控制中，机器人被视为**机械导纳**：接受运动输入，产生力输出。其典型实现架构是位置控制内环 + 力控制外环。

## 核心原理（Key Principles）

- **因果关系反转**：测量运动（位置/速度）→ 计算期望力 → 施加力输出
- **内环/外环架构**：内环是高带宽位置控制器，外环通过调节期望轨迹来实现期望力响应
- **对环境的假设**：导纳控制假设环境是"阻抗"（接受力，产生运动）

## 与阻抗控制的对比

| 特性 | 导纳控制 | [[concepts/impedance-control|阻抗控制]] |
|------|----------|----------|
| 因果 | 运动 → 力 | 力 → 运动 |
| 适用 | 重型、高减速比、非反向可驱 | 轻量、低减速比、反向可驱 |
| 稳定性 | 在刚性环境中更稳定 | 在柔性环境中更稳定 |
| 实现 | 需要力/力矩传感器 | 可利用本体力矩控制 |

## 工业应用场景

导纳控制特别适用于：
- 大型工业焊接机器人（高刚度本体，需要柔顺行为）
- 重型搬运机器人的人机协作改造
- 需要通过力传感器精确控制接触力的场景（如精密装配）

## 参考文献（References）

- [阻抗控制入门介绍](raw/articles/2026-06-24-impedance-control-intro.md)
