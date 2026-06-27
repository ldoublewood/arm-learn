# VLA (Vision-Language-Action) Training for XLeRobot
**URL:** http://localhost:3000/s/f19236ab (source: https://xlerobot.readthedocs.io)
**Date captured:** 2026-06-27
**Source type:** documentation / tutorial

---

## Overview

This tutorial guides through training a Vision-Language-Action (VLA) model to control XLeRobot arms autonomously. Covers teleoperation (leader arm + VR), dataset recording, policy training with ACT, and deployment.

## What You'll Learn

1. How to teleoperate and record demonstration datasets for XLeRobot
2. How to train and evaluate your policy
3. How to make the policy work effectively

## 1. Hardware Setup

### Camera Setup
- XLeRobot has three cameras: two wrist cameras and one head camera
- Head camera angle must be consistent between data collection and inference
- Use `lerobot-find-cameras opencv` to verify camera setup

### Servo Control
- Head servos can be controlled via RoboCrew library for repeatable camera positioning
- `ServoControler` class with `turn_head_to_vla_position()` method

## 2. Dataset Recording

### 2.1 Single Arm with Leader Arm
- Uses `so101_follower` robot type and `so101_leader` teleoperator
- Single arm is sufficient for simple pick-and-place tasks
- Fewer servos and cameras = easier for model to learn

Recording command:
```bash
python lerobot/record.py \
  --robot.type=so101_follower \
  --robot.port=/dev/right_arm \
  --robot.cameras="{ head: {...}, right: {...} }" \
  --teleop.type=so101_leader \
  --teleop.port=/dev/ttyACM0 \
  --dataset.repo_id=your_huggingface_id/clear_table_single_arm \
  --dataset.num_episodes=50 \
  --dataset.single_task="Clear the table"
```

### 2.2 Dual Arm with VR
- Uses `xlerobot` robot type and `xlerobot_vr` teleoperator
- For more complex tasks requiring both arms
- VR controls: Reset Position, Early Exit, Delete Episode, Stop Recording

### Data Quality Tips
1. Check for dropped frames (monitor bandwidth/CPU)
2. Avoid redundant frames (use early exit when task complete)
3. Maintain scene consistency (no extra moving objects/people in view)

## 3. Policy Training
- Uses LeRobot training pipeline
- Reference: HuggingFace LeRobot imitation learning tutorials

## 4. Model Deployment

### Local Deployment (Raspberry Pi)
- Lightweight ACT policy can run directly on robot's Raspberry Pi
- Simple `lerobot/record.py` script with policy parameter

### Remote Deployment (GPU Server)
- For resource-intensive policies (SmolVLA, Pi0.5)
- Uses LeRobot async inference: policy server on GPU PC, client on robot
- Server command:
```bash
python -m lerobot.async_inference.policy_server --host=0.0.0.0 --port=8080
```
- RoboCrew library provides async client as LLM agent tool

## Key Technologies Mentioned
- **ACT (Action Chunking Transformer)**: Lightweight VLA policy
- **SmolVLA**: Resource-intensive VLA policy
- **Pi0.5**: Advanced policy requiring GPU
- **LeRobot**: HuggingFace robot learning framework
- **RoboCrew**: XLeRobot control library
- **XLeRobot**: Dual-arm mobile manipulator platform
