# OpenArm — 面向物理 AI 研究的全开源人形机械臂
**URL:** https://github.com/enactic/openarm
**Date captured:** 2026-06-24
**Source type:** GitHub repository (Enactic)
**Stars:** 2605 | **License:** Apache-2.0 (软件), CERN-OHL-S-2.0 (硬件)

---

## 项目概述

OpenArm 是一个 7 自由度开源人形机械臂，专为物理 AI 研究（Physical AI Research）设计，适用于接触密集型环境部署。具有高反向驱动性（backdrivability）和柔顺性，人机交互安全。双臂完整系统约 $6,500 USD。

## 技术特点
- **人体比例尺寸**：符合人体工学的臂展和关节配置
- **安全与柔顺**：高反向驱动性，适合人机协作
- **实用负载能力**：满足真实世界应用需求
- **标准化评估环境（OpenArm Cell）**：统一背景、光照、相机布局，确保全球研究结果可复现

## 开源仓库体系（模块化设计）

| 仓库 | 说明 | 许可证 |
|------|------|--------|
| **openarm_hardware** | 完整 CAD 数据：STL、STEP、Fusion 360 装配体 | CERN-OHL-S-2.0 |
| **openarm_description** | URDF/xacro 机器人描述文件 | Apache-2.0 |
| **openarm_can** | CAN 总线底层电机通信控制库 | Apache-2.0 |
| **openarm_ros2** | ROS2 集成包和节点 | Apache-2.0 |
| **openarm_teleop** | 遥操作包：单边 + 双边力反馈控制 | Apache-2.0 |
| **openarm_isaac_lab** | Isaac Lab 仿真环境和训练任务 | Apache-2.0 |
| **openarm_mujoco** | MuJoCo 物理仿真模型和资产 | Apache-2.0 |
| **openarm_dataset** | 数据格式、录制工具和 Python API | Apache-2.0 |
| **dora-openarm** | Dora 数据流节点：数据采集、推理、遥操作 | Apache-2.0 |

## 覆盖领域

### 机械/硬件
- 完整 CAD 设计文件（Fusion 360 原始装配体 + STEP + STL）
- 可自行制造或通过认证制造商购买成品

### 软件
- CAN 总线底层驱动
- ROS2 完整集成（MoveIt2 运动规划）
- Python API

### 算法
- 重力补偿（Gravity Compensation）
- 双边力反馈遥操作（Bilateral Teleoperation）
- 模仿学习（Imitation Learning）
- 强化学习（Reinforcement Learning）

### 仿真
- MuJoCo 物理仿真
- Isaac Lab 仿真环境
- URDF/xacro 模型描述

### 数据
- 标准化数据集格式
- 数据录制工具
