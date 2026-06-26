# reBot-DevArm — 面向开发者的全开源机械臂
**URL:** https://github.com/Seeed-Projects/reBot-DevArm
**Date captured:** 2026-06-24
**Source type:** GitHub repository (Seeed Studio)
**Stars:** 3693 | **License:** CERN-OHL-W-2.0

---

## 项目概述

reBot-DevArm 是 Seeed Studio 推出的"真正全开源"机械臂项目，旨在降低具身智能（Embodied AI）的学习门槛。项目不仅开源代码，还无保留地开源所有硬件设计文件。

提供两个版本：
- **reBot Arm B601 DM**（达妙电机版）：负载 1.5kg，臂展 767mm，重约 4.5kg，24V 供电
- **reBot Arm B601 RS**（Robstride 电机版）：负载 2.5kg，臂展 754mm，重约 6.7kg，48V 供电

两者均为 6 DOF + 1 Gripper，重复定位精度 < 0.2mm。

## 开源内容

### 硬件
- 钣金件源文件 + 3D 打印件源文件（STEP 格式）
- 完整 BOM 清单（精确到每颗螺丝的规格和购买链接）
- 组装视频和详细步骤
- 真机性能测试参考数据

### 软件与算法
- **Python SDK (Motorbridge)**：一站式电机读写控制，支持 Robstride、Damiao、Mota、Gaoqing、Hexfellow 等多品牌电机
- **ROS2 集成**：运动学、轨迹规划、重力补偿
- **Pinocchio 集成**：正/逆运动学、重力补偿
- **LeRobot 集成**：HuggingFace 模仿学习训练框架
- **Isaac Sim 仿真**（开发中）
- **深度相机集成**：基于 YOLO + 深度相机的视觉抓取演示
- **reSpeaker 语音集成**：4 麦阵列语音控制

### 生态适配状态
| 生态 | 状态 |
|------|------|
| Python SDK | ✅ 持续优化 |
| ROS2 | ✅ 完成 |
| Pinocchio | ✅ 完成 |
| LeRobot | ✅ 完成 |
| Isaac Sim | 🚧 进行中 |
| 深度相机抓取 | ✅ 完成 |
| 语音控制 | ✅ 完成 |
| 免费系列课程 | ⏳ 计划中 |

## 购买渠道
提供 5 种套件方案：电机套件、结构件套件、夹爪完整套件、整机完整套件、成品组装机械臂。可通过 Seeedstudio 官网或淘宝矽递科技旗舰店购买。
