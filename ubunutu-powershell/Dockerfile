FROM ubuntu:latest
MAINTAINER Uttesh Kumar T.H. <uttesh.com>
ENV DEBIAN_FRONTEND noninteractive

# Install dependencies and clean up
RUN apt-get -y update \
    && apt-get install -y --no-install-recommends \
        apt-utils \
        ca-certificates \
        curl apt-utils wget unzip \
		libicu55 \
		dos2unix \ 
        apt-transport-https \
    && rm -rf /var/lib/apt/lists/*

RUN apt-get update && apt-get install -y sudo && rm -rf /var/lib/apt/lists/*

# Import the public repository GPG keys for Microsoft
RUN curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

# Register the Microsoft Ubuntu 16.04 repository
RUN curl -o /etc/apt/sources.list.d/microsoft.list https://packages.microsoft.com/config/ubuntu/16.04/prod.list

# Install powershell from Microsoft Repo
RUN apt-get -y update \
    && apt-get install -y --no-install-recommends \
	powershell \
	krb5-multidev \
	libkrb5-dev \
	gss-ntlmssp
	
CMD [ "pwsh" ]