# ROS 2 Vehicle Control Interface

This project provides a ROS 2-based interface to control a vehicle's **motor (drive)**, **steering**, **dumper**, and **bucket** using the `/cmd_vel` topic. A subscriber node listens to velocity commands and sends them to the hardware (e.g., via serial).

## Prerequisites

- ROS 2 (tested with Humble)
- `colcon` build tool
- Python 3

## Setup & Build Instructions

### 1. Navigate to the workspace

### 2. Build the project (if not already built)

```bash
colcon build
```

### 3. Source the workspace

```bash
source install/setup.bash
```

> You must source the workspace in every new terminal.

## Run the Node

```bash
ros2 run subscriber subscriber
```

## Control Commands

Open a **new terminal**, source the workspace again, and publish commands to `/cmd_vel`.

### Axis Mapping

| Axis        | Function                 |
|------------|--------------------------|
| `linear.x`  | Motor (forward/backward) |
| `angular.z` | Steering (left/right)    |
| `linear.y`  | Dumper (up/down)         |
| `linear.z`  | Bucket (up/down)         |

---

### Motor Control

```bash
# Drive forward
ros2 topic pub -1 /cmd_vel geometry_msgs/Twist "{linear: {x: 1.0}}"

# Drive backward
ros2 topic pub -1 /cmd_vel geometry_msgs/Twist "{linear: {x: -1.0}}"

# Stop
ros2 topic pub -1 /cmd_vel geometry_msgs/Twist "{linear: {x: 0.0}}"
```

---

### Steering Control

```bash
# Left
ros2 topic pub -1 /cmd_vel geometry_msgs/Twist "{angular: {z: -1.0}}"

# Right
ros2 topic pub -1 /cmd_vel geometry_msgs/Twist "{angular: {z: 1.0}}"

# Center
ros2 topic pub -1 /cmd_vel geometry_msgs/Twist "{angular: {z: 0.0}}"
```

---

### Dumper Control

```bash
# Up
ros2 topic pub -1 /cmd_vel geometry_msgs/Twist "{linear: {y: 1.0}}"

# Down
ros2 topic pub -1 /cmd_vel geometry_msgs/Twist "{linear: {y: -1.0}}"
```

---

### Bucket Control

```bash
# Up
ros2 topic pub -1 /cmd_vel geometry_msgs/Twist "{linear: {z: -1.0}}"

# Down
ros2 topic pub -1 /cmd_vel geometry_msgs/Twist "{linear: {z: 1.0}}"
```

---

## Notes

- `-1` means the message is published **once**
- Ensure your hardware interface (e.g., serial port) is properly configured
