# ROS 2 Humble + Gazebo Classic 11 — DevContainer Template

This repository provides a ready-to-use template for developing with:

* ROS 2 Humble
* Gazebo Classic 11
* VS Code Dev Containers
* A minimal ROS 2 workspace (`ros2_ws`) prepared for building

The goal is to provide a reproducible and simple environment for developing, testing, and simulating ROS 2 projects with Gazebo Classic.

## Project Structure

```
ros2_humble_gazebo_classic11_container_template/
├── .devcontainer/
│   ├── devcontainer.json     # VS Code DevContainer configuration
│   └── Dockerfile            # Docker image with ROS 2 + Gazebo Classic
├── README.md                 # This file
└── ros2_ws/
    └── src/
        └── your_packages/    # Place your ROS 2 packages here
```

## Features

* ROS 2 Humble Desktop pre-installed
* Gazebo Classic 11 (gazebo11, libgazebo11-dev)
* ROS ↔ Gazebo integration via `gazebo_ros_pkgs`
* Ready-to-use ROS 2 workspace located at `/ros2_ws`
* Automatic VS Code extensions (ROS, C++, Python)
* GUI support (Gazebo, RViz, rqt)
* Fully isolated and reproducible environment using Docker and Dev Containers

## Note About First-Time Startup

Gazebo Classic 11 and its ROS integration (`gazebo_ros_pkgs`) are built from source inside the Docker image.
Because of this, **the very first build and startup of the DevContainer may take longer than usual** as all components are compiled and configured.

Subsequent launches will be much faster since the environment is already built.

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/<your-user>/ros2_humble_gazebo_classic11_container_template.git
cd ros2_humble_gazebo_classic11_container_template
```

### 2. Open the folder in VS Code

```bash
code .
```

### 3. Open inside the DevContainer

VS Code should automatically propose:

Reopen in Container

If not:

```
Ctrl+Shift+P → Dev Containers: Rebuild and Reopen in Container
```

Once the container is running, the terminal should open in:

```
root@container:/ros2_ws#
```

## Building the ROS 2 Workspace

Place your packages in:

```
ros2_ws/src/your_packages
```

Inside the container:

```bash
cd /ros2_ws
colcon build --symlink-install
source install/setup.bash
```

## Testing Gazebo Classic and ROS 2

Run Gazebo Classic:

```bash
gazebo
```

List ROS 2 topics:

```bash
ros2 topic list
```

Run RViz2:

```bash
rviz2
```

## License

This project is released under the [BSD 3-Clause License](LICENSE).