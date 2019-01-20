FROM ubuntu

# user / group args
ARG UNAME=atlas
ARG UID=1000
ARG GID=1000

# create atlas user
RUN groupadd -g ${GID} -o ${UNAME}
RUN useradd -u ${UID} -g ${GID} -d /home/${UNAME} -m -s /bin/bash ${UNAME}
ENV HOME /home/${UNAME}
WORKDIR /home/${UNAME}

# START install

# non interactive installs
ENV DEBIAN_FRONTEND noninteractive

# add 32bit arch since we're on 64bit OS
RUN dpkg --add-architecture i386

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install openssh-client -y

# END install

# create rook fs mount path
RUN mkdir /var/lib/atlas-server
RUN chmod a+x /var/lib/atlas-server

USER ${UNAME}