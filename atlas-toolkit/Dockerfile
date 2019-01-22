FROM ubuntu

# non interactive installs
ENV DEBIAN_FRONTEND noninteractive

# add 32bit arch since we're on 64bit OS
RUN dpkg --add-architecture i386

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install openssh-client -y

# END install


