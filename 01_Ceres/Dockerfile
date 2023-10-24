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