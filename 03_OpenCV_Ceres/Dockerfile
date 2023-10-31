FROM ubuntu:20.04

# Install required libraries for build
RUN apt-get update 

RUN ln -fs /usr/share/zoneinfo/Europe/Paris /etc/localtime
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y tzdata
RUN dpkg-reconfigure --frontend noninteractive tzdata

RUN apt-get install -y \
	g++ cmake \
	libgoogle-glog-dev libgflags-dev libatlas-base-dev libeigen3-dev \
	libsuitesparse-dev wget git libgtk2.0-dev pkg-config \
	libavcodec-dev libavformat-dev libswscale-dev \
	python3-dev python3-numpy libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff-dev libdc1394-22-dev \
	libcanberra-gtk-module libcanberra-gtk3-module

# Clone, build and install OpenCV
RUN git clone https://github.com/opencv/opencv.git && \
    cd /opencv && mkdir build && cd build && \
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
RUN make -j3
RUN make install

#Cleanning docker image
WORKDIR /home
RUN rm -rf ceres-bin
RUN rm -rf ceres-solver-2.2.0.tar.gz
RUN rm -rf ceres-solver-2.2.0