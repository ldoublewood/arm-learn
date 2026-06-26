# 牧卫机器人 (Mockway Robotics) — 开源六轴协作机械臂系统
**URL:** https://github.com/Jelatine/mockway_robotics
**Date captured:** 2026-06-24
**Source type:** GitHub repository
**Stars:** 139 | **License:** MIT

---

## 项目概述

牧卫机器人是一个开源六轴协作机械臂系统，包含机械结构、电路和软件的完整方案。使用 JellyCAD 进行参数化建模，结构件可 3D 打印。复刻成本约 4,200 元人民币，是极具性价比的开源机械臂方案。

## 开源内容

### 机械结构
- **JellyCAD 参数化建模**：模型参数在 `/jellycad_src` 目录，可参数化调整结构
- **3D 打印结构件**：已上传 MakerWorld，可直接打印
- **详细组装指南**

### 电路
- 电气拓扑图
- 使用维特 USB-CAN 模块（串口 921600 bps，CAN 1M bps）

### 软件与控制
- **电机调试 GUI**：单电机运动调试和关节零点标定界面
- **力矩补偿**：实时重力补偿和前馈力矩补偿
- **MoveIt! 集成**：ROS2 Jazzy + MoveIt! 运动规划
- **完整 Bringup**：move_group + servo 伺服控制
- **Web 前端**：浏览器控制界面（http://localhost:8080）
- **OpenClaw 应用**：自然语言控制机械臂（LLM + skill 指令）

## 物料成本

| 项目 | 约成本 |
|------|--------|
| 电机 | ≈4,000 元 |
| 3D 打印件 | ≈20 元 |
| USB2CAN | ≈73 元 |
| 电源 | ≈100 元 |
| 螺丝及工具 | <40 元 |
| **总计** | **≈4,200 元** |

## 软件环境
- **OS**: Ubuntu 24.04
- **ROS2**: Jazzy + MoveIt!
- **CAN**: 维特 USB-CAN 模块
- **额外依赖**: Lua 5.4（用于 bringup），Pinocchio（动力学计算）

## 安全注意事项
项目特别强调了力矩模式的安全操作：
1. 确保机械结构与 URDF 模型一致
2. 必须执行关节零点标定
3. 先以位置模式运行，对比实际力矩与算法计算力矩
4. 初次测试使用重力补偿模式 + 增加电机阻尼参数（kd=1）
5. 3D 打印件建议 ≥40% 填充率，使用 Gyroid 填充图案

## 技术栈
- **语言**: C++, Python, Lua, Vue.js
- **框架**: ROS2, MoveIt2, Pinocchio
- **建模**: JellyCAD（自研参数化 CAD）
- **通信**: CAN 总线 (SocketCAN)
- **前端**: Web 界面 (Vue.js)
