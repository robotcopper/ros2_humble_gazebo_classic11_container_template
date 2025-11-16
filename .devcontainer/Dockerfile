# Base image with ROS 2 Humble Desktop
FROM osrf/ros:humble-desktop

ENV DEBIAN_FRONTEND=noninteractive

###########################################
# Create workspace
###########################################
RUN mkdir -p /ros2_ws/src
WORKDIR /ros2_ws

###########################################
# 🔧 Basic tools and utilities
###########################################
RUN apt-get update && apt-get install -y \
    software-properties-common \
    wget \
    lsb-release \
    gnupg2

###########################################
# Add the Gazebo Classic repository
###########################################
RUN add-apt-repository -y ppa:openrobotics/gazebo11-gz-cli && \
    apt-get update

###########################################
# Install Gazebo Classic 11
###########################################
RUN apt-get install -y --no-install-recommends \
    gazebo11 \
    libgazebo11-dev && \
    rm -rf /var/lib/apt/lists/*

ENV CMAKE_PREFIX_PATH=/usr/share/gazebo-11/cmake:$CMAKE_PREFIX_PATH

###########################################
# ROS 2 development tools
###########################################
RUN apt-get update && apt-get install -y \
    python3-colcon-common-extensions \
    build-essential \
    git \
    ros-humble-moveit \
    ros-humble-ros2-control \
    && rm -rf /var/lib/apt/lists/*

###########################################
# Clone ROS ↔ Gazebo packages
###########################################
WORKDIR /ros2_ws/src

RUN git clone -b ros2 https://github.com/ros-simulation/gazebo_ros_pkgs.git && \
    git clone -b humble https://github.com/ros-controls/gazebo_ros2_control.git

###########################################
# Install additional ROS 2 packages
###########################################
RUN apt-get update && apt-get install -y --no-install-recommends \
    ros-humble-navigation2 \
    ros-humble-nav2-bringup \
    ros-humble-slam-toolbox \
    ros-humble-ros2-control \
    ros-humble-ros2-controllers \
    ros-humble-robot-localization \
    ros-humble-moveit \
    ros-humble-topic-based-ros2-control \
    ros-humble-tf2-geometry-msgs \
    ros-humble-nav-msgs \
    ros-humble-std-srvs \
    ros-humble-joint-state-publisher \
    ros-humble-joint-state-publisher-gui \
    ros-humble-xacro \
    ros-humble-camera-info-manager \
    ros-humble-imu-tools \
    && rm -rf /var/lib/apt/lists/*

###########################################
# Build workspace
###########################################
WORKDIR /ros2_ws
ENV MAKEFLAGS="-j4"

RUN . /opt/ros/humble/setup.sh && \
    colcon build --symlink-install --executor sequential --parallel-workers 1

###########################################
# 🧠 Environment setup
###########################################
RUN echo "source /opt/ros/humble/setup.bash" >> /root/.bashrc && \
    echo "source /ros2_ws/install/setup.bash" >> /root/.bashrc && \
    echo "source /usr/share/gazebo/setup.sh" >> /root/.bashrc

CMD ["bash"]

