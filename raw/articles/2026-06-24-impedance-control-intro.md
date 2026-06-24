# An Introduction to Impedance Control for Robotic Manipulators

**Source URL:** https://example.com/impedance-control-intro (sample)
**Date captured:** 2026-06-24
**Source type:** web article

---

## What is Impedance Control?

Impedance control is an approach to dynamic control of robotic manipulators pioneered by Neville Hogan in 1985. Unlike traditional position control which commands exact joint angles, impedance control regulates the dynamic relationship between the manipulator's motion and the forces it exerts on the environment.

The core idea: instead of controlling position OR force exclusively, impedance control allows the robot to behave like a mass-spring-damper system. When the environment pushes on the robot, the robot yields with a specified stiffness and damping, rather than fighting to maintain an exact position.

## The Mathematical Model

The target impedance is typically expressed as:

    M(x_ddot - x_ddot_d) + B(x_dot - x_dot_d) + K(x - x_d) = F_ext

Where:
- M is the desired inertia matrix
- B is the desired damping matrix  
- K is the desired stiffness matrix
- x is actual position, x_d is desired position
- F_ext is the external force

## Key Applications

1. **Assembly tasks** - The robot can comply when inserting parts, preventing jamming and damage.

2. **Polishing and grinding** - Maintaining consistent force while following curved surfaces.

3. **Human-robot interaction** - Making the robot safe and compliant when humans are nearby.

4. **Unknown environments** - The robot can adapt to uncertain contact conditions.

## Relationship to Admittance Control

Impedance control assumes the robot is a mechanical impedance (accepts force input, produces motion output). Admittance control is the dual: the robot is a mechanical admittance (accepts motion input, produces force output).

Impedance control is preferred for lightweight, backdrivable robots. Admittance control is preferred for heavy, non-backdrivable industrial arms.

## ROS2 Implementation

The `ros2_control` framework provides impedance control implementations through its controller interface. Key packages include:
- `joint_trajectory_controller`
- `force_torque_sensor_broadcaster`
- `impedance_control` (community package)
