FROM ros:melodic-robot

COPY packages /home/k4r_sanbox-controller_ws/src
# Install prerequisites
RUN apt-get update && apt-get install -y \
  apt-utils \
  python-pip \
  ros-melodic-tf2-geometry-msgs

RUN pip install flask future
#RUN pip install tf2-geometry-msgs

# Install dependencies
WORKDIR /home/k4r_sanbox-controller_ws

RUN rosdep install --from-paths src --ignore-src -r -y


# Build catkin workspace
RUN . /opt/ros/melodic/setup.sh && catkin_make

# TODO: Change the hard code
ENV ROS_MASTER_URI=http://192.168.0.2:11311
ENV ROS_IP=192.168.0.42

SHELL ["/bin/bash", "-c"]
COPY ./entrypoint.bash /entrypoint.bash
RUN chmod +x /entrypoint.bash
