FROM ros:noetic

RUN apt-get update \
 && apt-get install -y --no-install-recommends \
    git wget nano libomp-dev build-essential python3-pip \
    libopencv-dev \
    ros-${ROS_DISTRO}-eigen-conversions ros-${ROS_DISTRO}-cv-bridge \
    ros-${ROS_DISTRO}-image-transport-plugins \
    ros-${ROS_DISTRO}-pcl-ros ros-${ROS_DISTRO}-rviz \
 && apt-get clean && rm -rf /var/lib/apt/lists/*

WORKDIR /root
RUN git clone https://github.com/koide3/Sophus.git -b fast_livo \
  && mkdir Sophus/build \
  && cd Sophus/build \
  && cmake .. \
  && make -j$(nproc) \
  && make install

RUN cp -R /usr/local/include/sophus /usr/include/

WORKDIR /root
RUN git clone https://github.com/Livox-SDK/Livox-SDK.git \
  && mkdir -p Livox-SDK/build \
  && cd Livox-SDK/build \
  && cmake .. \
  && make -j$(nproc) \
  && make install \
  && rm -rf /root/Livox-SDK

RUN mkdir -p /root/catkin_ws/src
WORKDIR /root/catkin_ws/src
RUN /bin/bash -c '. /opt/ros/${ROS_DISTRO}/setup.bash; catkin_init_workspace'

RUN git clone https://github.com/koide3/rpg_vikit.git -b fast_livo
RUN git clone https://github.com/Livox-SDK/livox_ros_driver.git
COPY . /root/catkin_ws/src/FAST-LIVO

WORKDIR /root/catkin_ws
RUN /bin/bash -c '. /opt/ros/${ROS_DISTRO}/setup.bash; catkin_make -DCMAKE_BUILD_TYPE=Release'

RUN sed -i "6i source \"/root/catkin_ws/devel/setup.bash\"" /ros_entrypoint.sh

WORKDIR /

ENTRYPOINT ["/ros_entrypoint.sh"]
CMD ["bash"]
