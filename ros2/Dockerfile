# ROS 2 Humble on Ubuntu 22.04
FROM osrf/ros:humble-desktop

SHELL ["/bin/bash", "-c"]

# Install handy tools
RUN apt-get update && apt-get install -y --no-install-recommends

# Source ROS automatically for interactive shells
RUN echo 'source /opt/ros/humble/setup.bash' >> /root/.bashrc

# Use image’s entrypoint that sources ROS env
ENTRYPOINT ["/ros_entrypoint.sh"]
CMD ["bash"]