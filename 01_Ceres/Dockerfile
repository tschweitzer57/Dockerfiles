FROM ubuntu:20.04
RUN apt-get update 

RUN ln -fs /usr/share/zoneinfo/Europe/Paris /etc/localtime
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y tzdata
RUN dpkg-reconfigure --frontend noninteractive tzdata
RUN apt-get install cmake -y

RUN apt-get install libgoogle-glog-dev libgflags-dev -y
RUN apt-get install libatlas-base-dev -y
RUN apt-get install libeigen3-dev -y
RUN apt-get install libsuitesparse-dev -y
RUN apt-get install wget -y

WORKDIR /home
RUN wget http://ceres-solver.org/ceres-solver-2.2.0.tar.gz
RUN tar zxf ceres-solver-2.2.0.tar.gz
RUN mkdir ceres-bin

WORKDIR /home/ceres-bin
RUN cmake ../ceres-solver-2.2.0
RUN make -j3
RUN make install