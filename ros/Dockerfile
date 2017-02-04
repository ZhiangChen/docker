# Install ROS Indigo
# copy from https://github.com/osrf/docker_images/blob/d9efe4367b9d376fd97a154bdaba896ca0382645/ros/indigo/indigo-desktop-full/Dockerfile
FROM osrf/ros:indigo-desktop

RUN apt-get update && apt-get install -y \
	ros-indigo-desktop-full=1.1.4-0* \
	&& rm -rf /var/lib/apt/lists/* 

# Now create the ros user itself
RUN adduser --gecos "ROS User" --disabled-password ros

# And, as that user...
USER ros

# HOME needs to be set explicitly. Without it, the HOME environment variable is
# set to "/"
RUN HOME=/home/ros rosdep update

# Create a ROS workspace for the ROS user.
RUN mkdir -p /home/ros/catkin_ws/src
RUN /bin/bash -c '. /opt/ros/indigo/setup.bash; catkin_init_workspace /home/ros/catkin_ws/src'
RUN /bin/bash -c '. /opt/ros/indigo/setup.bash; cd /home/ros/catkin_ws; catkin_make'
RUN echo "source ~/catkin_ws/devel/setup.bash" >> /home/ros/.bashrc
RUN echo "export ROS_WORKSPACE='/home/ros/catkin_ws'" >> /home/ros/.bashrc

USER root