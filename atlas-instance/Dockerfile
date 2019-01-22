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
    # locales
    apt-get install -y --no-install-recommends locales && \
    sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && \
    dpkg-reconfigure --frontend=noninteractive locales && \
    update-locale LANG=en_US.UTF-8 && \
    # basic deps
    apt-get install -y --no-install-recommends lib32gcc1 gpg-agent software-properties-common apt-transport-https wget && \
    # steamcmd
    su -p -l ${UNAME} -c 'wget -qO- "https://steamcdn-a.akamaihd.net/client/installer/steamcmd_linux.tar.gz" | tar zxvf -' && \
    # clean
    apt-get autoremove -y --purge software-properties-common && \
    apt-get autoremove -y --purge && \
    apt-get clean -y && \
    rm -rf /home/${UNAME}/.cache && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# END install

# create rook fs mount path
#RUN mkdir /var/lib/atlas-server && \
#    chmod a+x /var/lib/atlas-server && \
#    chown atlas:atlas /var/lib/atlas-server

# locale env
ENV LANG en_US.UTF-8
ENV LC_ALL en_US.UTF-8

COPY ./bin /usr/local/bin
RUN chmod a+x /usr/local/bin/*

# USER ${UNAME}