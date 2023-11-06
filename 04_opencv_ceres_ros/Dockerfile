FROM osrf/ros:humble-desktop

# Install required libraries for build
RUN apt update 

RUN ln -fs /usr/share/zoneinfo/Europe/Paris /etc/localtime
RUN DEBIAN_FRONTEND=noninteractive 
RUN apt install -y tzdata
RUN dpkg-reconfigure --frontend noninteractive tzdata

RUN apt install -y \
    libgoogle-glog-dev libatlas-base-dev \
    libsuitesparse-dev wget libgtk2.0-dev \
    libcanberra-gtk-module libcanberra-gtk3-module

# Clone, build and install OpenCV
RUN git clone https://github.com/opencv/opencv.git && \
    cd opencv && mkdir build && cd build && \
    cmake -D CMAKE_BUILD_TYPE=Release -D CMAKE_INSTALL_PREFIX=/usr/local .. && \
    make -j"$(nproc)" && \
    make install && \
    rm -rf /opencv

# Install Ceres from zipped file
WORKDIR /home
RUN wget http://ceres-solver.org/ceres-solver-2.2.0.tar.gz
RUN tar zxf ceres-solver-2.2.0.tar.gz
RUN mkdir ceres-bin

WORKDIR /home/ceres-bin
RUN cmake ../ceres-solver-2.2.0
RUN make -j4
RUN make install

#Cleanning docker image
WORKDIR /home
RUN rm -rf ceres-bin
RUN rm -rf ceres-solver-2.2.0.tar.gz
RUN rm -rf ceres-solver-2.2.0