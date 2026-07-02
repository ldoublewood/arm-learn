---
category: tool
version: ""
ecosystem: [Python, PyTorch, HuggingFace]
created: 2026-06-27
updated: 2026-06-27
tags: [imitation-learning, VLA, dataset, teleoperation]
---

# LeRobot

## 概述（Overview）

LeRobot 是 HuggingFace 推出的开源机器人学习框架，旨在降低机器人 AI 的入门门槛。它提供了一套完整的 PyTorch 模型、数据集和工具，专注于模仿学习（Imitation Learning）和强化学习（Reinforcement Learning），使任何人都能通过共享数据集和预训练模型参与到机器人 AI 的开发中。

- **开发者**: HuggingFace
- **许可证**: Apache-2.0
- **仓库**: https://github.com/huggingface/lerobot

## 核心功能（Key Features）

- **数据集录制**：支持多种机器人平台和相机配置的数据采集，统一数据格式便于共享
- **遥操作支持**：内置 leader arm、VR 等多种遥操作接口
- **策略训练**：提供 ACT、Diffusion Policy 等主流模仿学习算法实现
- **模型部署**：支持本地推理（边缘设备）和异步推理（GPU 服务器）两种模式
- **多机器人平台**：支持 XLeRobot、SO-101、Koch v1.1、Aloha 等多种机械臂平台
- **相机系统**：支持 OpenCV 相机和 Intel RealSense 深度相机

## 安装（Installation）

```bash
pip install lerobot
```

相机检测：
```bash
lerobot-find-cameras opencv     # OpenCV 相机
lerobot-find-cameras realsense  # Intel RealSense 深度相机
```

## 关键概念

### 数据集录制（Recording）
```bash
python lerobot/scripts/record.py \
  --robot.type=so101_follower \
  --robot.port=/dev/right_arm \
  --robot.cameras="{ head: {type: intelrealsense, ...}, right: {type: opencv, ...} }" \
  --teleop.type=so101_leader \
  --teleop.port=/dev/ttyACM0 \
  --dataset.repo_id=your_id/task_name \
  --dataset.num_episodes=50 \
  --dataset.single_task="描述任务"
```

### 策略训练（Training）
```bash
python lerobot/scripts/train.py \
  --dataset.repo_id=your_id/task_name \
  --policy.type=act
```

### 异步推理部署（Async Inference）
在 GPU 服务器端：
```bash
python -m lerobot.async_inference.policy_server --host=0.0.0.0 --port=8080
```
机器人端通过客户端连接服务器进行推理。

## 支持的策略（Supported Policies）

| 策略 | 算力需求 | 说明 |
|------|----------|------|
| ACT (Action Chunking Transformer) | 低（可在 Raspberry Pi 运行） | 轻量 VLA 策略，适合简单任务 |
| Diffusion Policy | 中 | 基于扩散模型的策略生成 |
| SmolVLA | 高（需 GPU） | 更强的 VLA 模型 |
| Pi0 / Pi0.5 | 高（需 GPU） | Physical Intelligence 前沿模型 |

## 与工业机械臂的关系（Relevance to Industrial Robotic Arms）

LeRobot 代表了机器人编程范式的转变——从手工编写控制代码到通过示范学习策略。在工业场景中：
- 可用于快速原型验证抓取、放置等操作任务
- 数据集共享机制促进社区协作和模型复用
- 但目前精度和可靠性尚未达到工业级标准，与 [[ros2-control|传统控制框架]] 互补使用

## 相关概念（Related Concepts）

- [[../concepts/imitation-learning]] — LeRobot 的核心训练范式
- [[../concepts/vla-vision-language-action]] — LeRobot 支持的 VLA 策略
- [[../concepts/impedance-control]] — 传统控制方法与学习方法的互补

## 参考文献（References）

- [VLA Training for XLeRobot](../../raw/docs/2026-06-27-vla-xlerobot.md)
- [LeRobot 官方文档](https://huggingface.co/docs/lerobot)
