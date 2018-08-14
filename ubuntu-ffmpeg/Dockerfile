FROM ubuntu:latest
MAINTAINER Uttesh Kumar T.H. <uttesh.com>
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get -y update && \
    apt-get -y upgrade && \
    apt-get install -y python-software-properties software-properties-common

# install avconv tools
RUN apt-get install -y libav-tools

RUN add-apt-repository -y ppa:jonathonf/ffmpeg-3
RUN apt-get update
RUN apt-get install -y ffmpeg libav-tools x264 x265
#ENTRYPOINT ["ffmpeg"]
	
CMD [ "ffmpeg"]