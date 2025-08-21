# ===== Base: ROS 2 Humble desktop on Ubuntu 22.04 =====
FROM osrf/ros:humble-desktop

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Locale (usually already set, but ensure it)
ENV LANG=C.UTF-8 \
    LC_ALL=C.UTF-8

# System deps, developer tools, and popular editors
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential cmake git curl gnupg lsb-release \
    python3-pip python3-venv \
    python3-colcon-common-extensions \
    python3-rosdep python3-vcstool \
    # OpenCV (C++ + Python)
    libopencv-dev python3-opencv \
    # Boost (headers + libs)
    libboost-all-dev \
    # Nav2 stack
    ros-humble-navigation2 ros-humble-nav2-bringup \
    && rm -rf /var/lib/apt/lists/*

# Initialize rosdep (safe to run in container)
RUN rosdep init 2>/dev/null || true && rosdep update

# Create a default workspace
ENV ROS_WS=/workspaces/ros2_ws
RUN mkdir -p ${ROS_WS}/src
WORKDIR ${ROS_WS}

# Standard ROS 2 entrypoint layering
# (The base image already has /ros_entrypoint.sh, we extend it with our workspace overlay)
RUN echo 'source "/opt/ros/${ROS_DISTRO}/setup.bash"' >> /etc/bash.bashrc \
 && echo 'if [ -f "${ROS_WS}/install/setup.bash" ]; then source "${ROS_WS}/install/setup.bash"; fi' >> /etc/bash.bashrc

# Default command drops you into a bash with ROS sourced
CMD ["/bin/bash"]
