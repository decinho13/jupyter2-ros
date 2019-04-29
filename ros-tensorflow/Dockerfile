# Copyright (c) Jupyter Development Team.
# Distributed under the terms of the Modified BSD License.
ARG BASE_CONTAINER=decinho13/base-notebook2:scipy
FROM $BASE_CONTAINER

USER root

LABEL maintainer="Dennis Lubczyk"
RUN apt-get update && apt-get install -y \
python-rosdep python-rosinstall gnupg2 curl ca-certificates\
&& apt-get clean

# Install ROS
RUN sh -c 'echo "deb http://packages.ros.org/ros/ubuntu xenial main" > /etc/apt/sources.list.d/ros-latest.list'
RUN apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 421C365BD9FF1F717815A3895523BAEEB01FA116
RUN apt-get update && apt-get install -y ros-kinetic-ros-base \
 	&& rm -rf /var/lib/apt/lists/*

RUN pip install catkin_tools

# Configure ROS
RUN sudo rosdep init && sudo rosdep fix-permissions && rosdep update
RUN echo "source /opt/ros/kinetic/setup.bash" >> /root/.bashrc 

 
# Install MachineLearning Libraries
RUN conda install --quiet --yes \
    'tensorflow=1.12*' \
    'keras=2.2*' \
    'theano' \
    'pyspark' \
    'nltk' && \
    conda clean -tipsy 
RUN pip install elephas gym keras-rl opencv-python roslibpy
RUN pip install torchvision service_identity

RUN pip install bqplot pyyaml
RUN sudo apt-get install python-rospkg

RUN chown -R jovyan:0 /opt/ros  && chmod -R g=u  /opt/ros 
RUN chown -R jovyan:0  /etc  && chmod -R g=u /etc 
RUN chown -R jovyan:0  /home  && chmod -R g=u /home 

RUN pip install rospkg
RUN pip install jupyros
RUN echo "source /opt/ros/kinetic/setup.bash" >> /root/.bashrc 
RUN mkdir ros_ws && cd ros_ws && mkdir src && cd src && \
    git clone https://bitbucket.org/theconstructcore/openai_ros.git 
    
USER jovyan

