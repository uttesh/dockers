FROM ubuntu:latest
MAINTAINER Uttesh Kumar T.H. <uttesh.com>
ENV DEBIAN_FRONTEND noninteractive

# Version number of Guacamole to install
ENV GUACVERSION="0.9.14"

# Install Server Features

RUN apt-get -y update && \
    apt-get -y upgrade && \
    apt-get install -y build-essential libcairo2-dev libjpeg-turbo8-dev libpng-dev libossp-uuid-dev libavcodec-dev libavutil-dev \
libswscale-dev libfreerdp-dev libpango1.0-dev libssh2-1-dev libtelnet-dev libvncserver-dev libpulse-dev libssl-dev \
libvorbis-dev libwebp-dev jq curl wget
	
# Set SERVER to be the preferred download server from the Apache CDN
ENV SERVER="http://apache.org/dyn/closer.cgi?action=download&filename=guacamole/${GUACVERSION}"

# Download guacserver
RUN wget -O guacamole-server-${GUACVERSION}.tar.gz ${SERVER}/source/guacamole-server-${GUACVERSION}.tar.gz

# Extract Guacamole Files
RUN tar -xzf guacamole-server-${GUACVERSION}.tar.gz

# Make Directories
RUN mkdir /etc/guacamole

# Install guacd
WORKDIR "/guacamole-server-${GUACVERSION}"

RUN ./configure --with-init-dir=/etc/init.d 
RUN make 
RUN make install
RUN ldconfig

# Configure guacamole.properties
RUN echo "[server]" >> /etc/guacamole/guacd.conf
RUN echo "bind_host = 0.0.0.0" >> /etc/guacamole/guacd.conf
RUN echo "bind_port = 4822" >> /etc/guacamole/guacd.conf

EXPOSE 4822

ENV LOG_LEVEL="info"

CMD /usr/local/sbin/guacd -b 0.0.0.0 -L ${LOG_LEVEL} -f



