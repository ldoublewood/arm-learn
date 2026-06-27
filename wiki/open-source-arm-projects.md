---
category: reference
tags: [open-source, platforms, hardware, software, comparison]
created: 2026-06-24
updated: 2026-06-27
related: [[concepts/impedance-control]], [[tools/ros2-control]], [[concepts/imitation-learning]], [[concepts/vla-vision-language-action]], [[tools/lerobot]]
---

# 开源机械臂项目概览（Open Source Robotic Arm Projects）

本文汇总了当前最活跃、内容最齐全的开源机械臂项目，每个项目都覆盖了机械结构、硬件设计、软件SDK和控制算法中的多个方面。

## 项目对比总览

| 项目 | DOF | 负载 | 重复精度 | 软件生态 | 硬件开源 | 参考成本 |
|------|-----|------|----------|----------|----------|----------|
| reBot-DevArm | 6+1 | 1.5-2.5kg | <0.2mm | Python SDK, ROS2, LeRobot, Pinocchio, Isaac Sim | STEP+BOM完全开源 | 约 8,000 元 |
| OpenArm | 7 | 实用级 | — | ROS2, MuJoCo, Isaac Lab, CAN驱动, Dora | Fusion360+STEP全开源 | $6,500 (双臂) |
| Panthera-HT | 6 | — | — | C++/Python/ROS2, 阻抗控制, LeRobot | SolidWorks+钣金图全开源 | 低成本 |
| EL-A3 | 7 | — | — | Python SDK, ROS2+MoveIt2, Pinocchio | STEP+3MF+PCB全开源 | — |
| Mockway | 6 | — | — | ROS2+MoveIt2, Pinocchio, Web前端 | JellyCAD参数化+3D打印 | ≈4,200 元 |

---

## 1. reBot-DevArm (Seeed Studio)

**URL:** https://github.com/Seeed-Projects/reBot-DevArm
**Stars:** 3,693 | **License:** CERN-OHL-W-2.0

目前最全面的全栈开源机械臂项目，由 Seeed Studio 主导。

### 覆盖范围

**机械/硬件：**
- 钣金件 + 3D 打印件源文件（STEP 格式）
- 完整 BOM（每颗螺丝规格和购买链接）
- 两种版本：DM（达妙电机，1.5kg 负载）和 RS（Robstride，2.5kg 负载）

**软件：**
- Python SDK (Motorbridge)：统一多品牌电机控制接口
- ROS2：运动学、轨迹规划、[[concepts/impedance-control|重力补偿]]
- Web UI 控制界面

**算法与AI：**
- Pinocchio 动力学：正/逆运动学
- LeRobot 模仿学习框架
- YOLO + 深度相机视觉抓取
- Isaac Sim 仿真（开发中）
- 语音控制（reSpeaker 4麦阵列）

> 参考：[reBot-DevArm 详情](raw/articles/2026-06-24-rebot-devarm.md)

---

## 2. OpenArm (Enactic)

**URL:** https://github.com/enactic/openarm
**Stars:** 2,605 | **License:** Apache-2.0 / CERN-OHL-S-2.0

面向物理 AI 研究的 7-DOF 人形机械臂，最大的亮点是模块化的多仓库架构和完整的科研生态。

### 覆盖范围

**机械/硬件：**
- Fusion 360 原始装配体 + STEP + STL
- 高反向驱动性（backdrivability）设计，人机协作安全

**软件（9 个独立仓库）：**
- `openarm_can`：CAN 总线底层驱动
- `openarm_ros2`：ROS2 + MoveIt2 集成
- `openarm_teleop`：单边 + 双边力反馈遥操作
- `openarm_description`：URDF/xacro 模型

**算法与AI：**
- 重力补偿、双边力反馈遥操作
- 模仿学习（Imitation Learning）
- 强化学习（Reinforcement Learning）
- Isaac Lab + MuJoCo 双仿真环境

**数据：**
- 标准化数据集格式和录制工具
- OpenArm Cell 标准化评估环境（确保全球研究可复现）

> 参考：[OpenArm 详情](raw/articles/2026-06-24-openarm-enactic.md)

---

## 3. Panthera-HT (HighTorque Robotics)

**URL:** https://github.com/HighTorque-Robotics/Panthera-HT_Main
**Stars:** 80 | **License:** MIT

面向学生和创客的教育导向开源六轴机械臂，由高擎机电行星关节模组驱动。

### 覆盖范围

**机械/硬件：**
- SolidWorks 原始设计文件 + 钣金展开图 + 3D 打印 STL
- 钣金框架设计（低成本+高强度）
- 模块化设计，可自由更换电机和修改结构

**软件：**
- C++、Python、ROS2 三种控制方式
- 统一控制接口

**算法（最丰富的算法集合之一）：**
- 位置/速度/力矩控制
- [[concepts/impedance-control|阻抗控制（Impedance Control）]]
- 重力补偿 + 摩擦力补偿
- 主从遥操作（双臂）
- 拖动示教
- LeRobot 模仿学习
- 未来：视觉伺服、GraspNet、Pi0/Pi0.5 等前沿算法

> 参考：[Panthera-HT 详情](raw/articles/2026-06-24-panthera-ht.md)

---

## 4. EL-A3 (RobStride)

**URL:** https://github.com/RobStride/EDULITE_A3
**Stars:** 145 | **License:** MIT

7-DOF 桌面机械臂，最大特色是 SDK 与 ROS2 解耦设计，用户可按需选择。

### 覆盖范围

**机械/硬件：**
- STEP 模型 + 3MF 打印文件 + 线束图纸 + PCB 资料 + 组装 SOP
- 详细的每关节电机配置表（力矩/速度/位置限制）

**软件：**
- 纯 Python SDK：直接 CAN 通信，无需 ROS
- ROS2 控制系统：[[tools/ros2-control|ros2_control]] + MoveIt2 + pick_ik
- PyQt6 Debugger GUI：3D URDF 可视化 + 关节拖拽控制 + 实时监控

**算法：**
- Pinocchio 动力学（FK/IK/重力补偿）
- 多臂管理支持

> 参考：[EL-A3 详情](raw/articles/2026-06-24-edulite-a3.md)

---

## 5. 牧卫机器人 Mockway (Jelatine)

**URL:** https://github.com/Jelatine/mockway_robotics
**Stars:** 139 | **License:** MIT

开源六轴协作机械臂，最大亮点是使用自研 JellyCAD 参数化建模，复刻成本仅约 4,200 元。

### 覆盖范围

**机械/硬件：**
- JellyCAD 参数化建模（可参数化调整结构）
- 3D 打印结构件（已上传 MakerWorld）
- 电气拓扑图 + 维特 USB-CAN 模块

**软件：**
- 电机调试 GUI + 力矩补偿界面
- ROS2 Jazzy + MoveIt! 运动规划
- Web 前端控制界面（Vue.js）
- OpenClaw 自然语言控制（LLM + skill 指令）

**算法：**
- 重力补偿 + 前馈力矩补偿
- Pinocchio 动力学
- 特别注意安全：力矩模式下的安全操作流程

> 参考：[Mockway 详情](raw/articles/2026-06-24-mockway-robotics.md)

---

## 选型建议

| 需求场景 | 推荐项目 |
|----------|----------|
| 最全面的全栈学习（硬件+软件+AI） | **reBot-DevArm** |
| 物理 AI / 学术研究 | **OpenArm** |
| 算法学习（阻抗控制、遥操作等） | **Panthera-HT** |
| Python SDK 开发 + ROS2 双轨学习 | **EL-A3** |
| 最低成本复刻 + 参数化建模 | **牧卫 Mockway** |

## 相关概念

- [[concepts/impedance-control]] — 多个项目实现了阻抗控制
- [[concepts/admittance-control]] — 力控的对偶方法
- [[tools/ros2-control]] — ROS2 实时控制框架，多个项目使用
