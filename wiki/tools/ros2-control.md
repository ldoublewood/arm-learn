---
category: tool
version: "ROS 2 Humble / Rolling"
ecosystem: [ROS2]
created: 2026-06-24
updated: 2026-06-24
tags: [ros2, control, real-time]
---

# ros2_control

## 概述（Overview）

`ros2_control` 是 ROS 2 生态中的实时控制框架，为机器人控制器提供标准化的硬件抽象层（Hardware Abstraction Layer）和控制器管理器（Controller Manager）。它是 ROS 1 中 `ros_control` 的 ROS 2 继任者，由 ROS 2 核心团队维护。

- **许可证**：Apache 2.0
- **仓库**：https://github.com/ros-controls/ros2_control
- **文档**：https://control.ros.org/

## 关键功能（Key Features）

- **硬件抽象层（HAL）**：统一的硬件接口（`hardware_interface`），支持位置、速度、力矩、力等多种控制模式
- **控制器管理器**：动态加载、启动、停止、切换控制器，无需重启
- **实时安全**：支持实时线程执行控制循环
- **URDF 驱动配置**：从 URDF 模型直接生成控制配置
- **状态广播器**：`joint_state_broadcaster`、`force_torque_sensor_broadcaster` 等

## 安装（Installation）

```bash
sudo apt install ros-humble-ros2-control ros-humble-ros2-controllers
```

## 在工业机械臂中的应用

`ros2_control` 在工业机械臂领域的关键价值：

1. **标准控制器接口**：`joint_trajectory_controller` 提供标准轨迹跟踪
2. **力控支持**：通过 `force_torque_sensor_broadcaster` 和社区 `impedance_control` 包实现[[concepts/impedance-control|阻抗控制]]
3. **MoveIt 2 集成**：作为 MoveIt 2 的底层控制执行后端
4. **Gazebo 仿真**：与 Gazebo 无缝集成，实现仿真到真机的完整控制链

## 相关概念（Related Concepts）

- [[concepts/impedance-control]] — 阻抗控制可以通过 ros2_control 实现
- [[concepts/admittance-control]] — 导纳控制在重型工业臂上的实现也依赖 ros2_control 的力控接口

## 参考文献（References）

- [阻抗控制入门介绍](raw/articles/2026-06-24-impedance-control-intro.md)
- [ROS 2 Control 官方文档](https://control.ros.org/)
