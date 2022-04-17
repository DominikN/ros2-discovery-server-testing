FROM donowak/ros:galactic-ros-core

# install ros package
RUN apt-get update && apt-get install -y \
        ros-${ROS_DISTRO}-demo-nodes-cpp && \
    rm -rf /var/lib/apt/lists/*