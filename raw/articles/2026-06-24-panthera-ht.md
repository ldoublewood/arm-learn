# Panthera-HT — 面向学生和创客的开源六轴机械臂学习平台
**URL:** https://github.com/HighTorque-Robotics/Panthera-HT_Main
**Date captured:** 2026-06-24
**Source type:** GitHub repository (HighTorque Robotics)
**Stars:** 80 | **License:** MIT

---

## 项目概述

Panthera-HT 是一款开源六轴机械臂，使用高擎机电的行星关节模组。面向开发者提供可复用的统一控制接口，用于算法验证、课程实验、系统集成及二次开发的标准化软硬件实验平台。

项目源自 [Ragtime-LAB/Ragtime_Panthera](https://github.com/Ragtime-LAB/Ragtime_Panthera) 的开源工作，目标是以更低的价格让学生接触到高性能关节电机机械臂。

## 设计理念

### 低成本 + 高性能
- **钣金框架**：高性价比钣金作为整体框架，保证强度同时降低成本
- **3D 打印 + CNC 加工**：灵活的结构设计
- **高性能关节模组**：高擎机电行星关节模组，成本和性能平衡

### 完全开源 + 可扩展
- **结构开源**：SolidWorks 原始设计文件、钣金展开图、3D 打印 STL 文件
- **算法开源**：从底层控制到高级算法，所有代码完全开源
- **无限制修改**：可自由更换电机、修改结构、改变外观
- **模块化设计**：方便二次开发和功能扩展

### 教育导向
- 理解机械臂的机械结构设计
- 学习运动学和动力学算法
- 掌握电机控制和通信协议
- 实践从理论到实物的完整过程

## 控制功能

机械臂支持 C++、Python 和 ROS2 三种控制方式，具体功能包括：

- **位置/速度/力矩控制**
- **阻抗控制（Impedance Control）**
- **重力补偿模式**
- **重力补偿 + 摩擦力补偿模式**
- **主从遥操作（双臂）**
- **拖动示教**
- **LeRobot 框架数据采集和推理**

## 仓库体系

| 仓库 | 说明 |
|------|------|
| **Panthera-HT_Main** | 主项目仓库，项目介绍和功能总览 |
| **Panthera-HT_Model** | SolidWorks 设计文件、钣金图、3D 打印文件和 BOM |
| **Panthera-HT_SDK** | Python SDK 开发包，示例代码与开发工具链 |
| **Panthera-HT_ROS2** | ROS2 开发包，驱动、控制与仿真支持 |
| **Panthera-HT_lerobot** | LeRobot 集成包，模仿学习和机器人学习算法 |

## 未来规划

### 高级传统控制
- 视觉伺服控制
- GraspNet 抓取位姿估计
- 点云避障

### 具身智能方向
- Pi0、Pi0.5 等前沿算法集成
- RoboTWin2.0 适配
- 端到端学习
- 多模态感知与控制
