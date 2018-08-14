FROM ubuntu:latest
MAINTAINER Uttesh Kumar T.H. <uttesh.com>
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && apt-get install -y \
  supervisor wget make tomcat7 \
  libcairo2-dev libpng12-dev libossp-uuid-dev libfreerdp-dev \
  libpango1.0-dev libssh2-1-dev libtelnet-dev libvncserver-dev \
  libpulse-dev libssl-dev libvorbis-dev

RUN wget -O guacamole-0.9.13-incubating.war "http://apache.org/dyn/closer.cgi?action=download&filename=incubator/guacamole/0.9.13-incubating/binary/guacamole-0.9.13-incubating.war" && \
  wget -O guacamole-server-0.9.13-incubating.tar.gz "http://apache.org/dyn/closer.cgi?action=download&filename=incubator/guacamole/0.9.13-incubating/source/guacamole-server-0.9.13-incubating.tar.gz" && \
  tar -xzf guacamole-server-0.9.13-incubating.tar.gz && \
  cp guacamole-0.9.13-incubating.war /var/lib/tomcat7/webapps/guacamole.war && \
  cd guacamole-server-0.9.13-incubating && \
  ./configure --with-init-dir=/etc/init.d && \
  make && \
  make install && \
  update-rc.d guacd defaults && \
  ldconfig && \
  mkdir /usr/share/tomcat7/.guacamole && \
  mkdir -p /etc/guacamole /var/lib/guacamole/classpath && \
  ln -s /etc/guacamole/guacamole.properties /usr/share/tomcat7/.guacamole
  
ADD ./config/guacamole.properties /etc/guacamole/
ADD ./config/user-mapping.xml /etc/guacamole/
ADD ./supervisor/supervisor.conf /etc/supervisor/supervisor.conf
ADD ./supervisor/guacamole.sv.conf /etc/supervisor/conf.d/
ADD ./supervisor/tomcat7.sv.conf /etc/supervisor/conf.d/

ENV CATALINA_BASE /var/lib/tomcat7
ENV CATALINA_HOME /usr/share/tomcat7
ENV GUACAMOLE_HOME /etc/guacamole

EXPOSE 8080 
CMD ["supervisord", "-c", "/etc/supervisor/supervisor.conf"]
