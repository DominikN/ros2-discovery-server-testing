FROM ros:galactic-ros-core

# install ros package
RUN apt-get update && apt-get install -y \
        ros-$ROS_DISTRO-rmw-fastrtps-cpp \
        # ros-$ROS_DISTRO-rmw-fastrtps-dynamic-cpp \
        ros-${ROS_DISTRO}-demo-nodes-cpp && \
    rm -rf /var/lib/apt/lists/*

# ENV RMW_IMPLEMENTATION=rmw_fastrtps_dynamic_cpp
ENV RMW_IMPLEMENTATION=rmw_fastrtps_cpp