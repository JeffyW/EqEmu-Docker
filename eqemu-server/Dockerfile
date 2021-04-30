FROM debian:10

RUN apt-get -y update && apt-get -y install --no-install-recommends \
    build-essential \
    gcc \
    g++ \
    cmake \
    debconf-utils \
    git \
    git-core \
    libio-stringy-perl \
    lua5.1 \
    liblua5.1 \
    liblua5.1-dev \
    libluabind-dev \
    libmysql++ \
    libperl-dev \
    libperl5i-perl \
    libjson-perl \
    libsodium-dev \
    default-libmysqlclient-dev \
    libssl-dev \
    minizip \
    make \
    mariadb-client \
    open-vm-tools \
    unzip \
    uuid-dev \
    zlibc \
    curl \
    wget \
    ca-certificates \
# -- Needed? --
#libtool
#locales
#iputils-ping
#nano
# -- Not Needd? --
#cpp
#bash
# -- Not Found --
#libwtdbomysql-dev
#zlib-bin
#libsodium18
 && apt-get autoremove -y \
 && apt-get clean -y \
 && rm -rf /var/lib/apt/lists/*

ARG GROUP=eqemu
ARG USER=eqemu

#::: Create source and server directories
RUN groupadd $GROUP && useradd -g $GROUP -m $USER
ENV HOME /home/$USER

ARG SERVER_DIRECTORY=/home/$USER
# Install libsodium
RUN wget http://ftp.us.debian.org/debian/pool/main/libs/libsodium/libsodium-dev_1.0.11-2_amd64.deb -O $SERVER_DIRECTORY/libsodium-dev.deb \
 && wget http://ftp.us.debian.org/debian/pool/main/libs/libsodium/libsodium18_1.0.11-2_amd64.deb -O $SERVER_DIRECTORY/libsodium18.deb \
 && dpkg -i $SERVER_DIRECTORY/libsodium*.deb \
# Cleanup after ourselves
 && rm -f $SERVER_DIRECTORY/libsodium-dev.deb \
 && rm -f $SERVER_DIRECTORY/libsodium18.deb
	
WORKDIR /home/$USER/server
RUN cd $SERVER_DIRECTORY && mkdir server server_source server_build server_build_bots
# server/export server/logs server/shared server/Maps

RUN wget https://raw.githubusercontent.com/JeffyW/Server/master/utils/scripts/eqemu_server.pl -O $SERVER_DIRECTORY/server/eqemu_server.pl
#COPY eqemu_server.pl ./

RUN chown $USER:$GROUP *
