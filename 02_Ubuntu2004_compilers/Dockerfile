FROM ubuntu:20.04
LABEL maintainer="Thibault SCHWEITZER"
LABEL description="This Dockerfile installs gcc and all prerequisites to ubuntu 20.04"

RUN apt-get update
RUN apt install build-essential -y

RUN ln -fs /usr/share/zoneinfo/Europe/Paris /etc/localtime
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y tzdata
RUN dpkg-reconfigure --frontend noninteractive tzdata
RUN apt-get install gdb -y

RUN apt-get install cmake -y

RUN apt-get install python-is-python3 -y