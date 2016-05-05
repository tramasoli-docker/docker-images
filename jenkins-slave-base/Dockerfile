# This Dockerfile is used to build an image containing basic stuff to be used as a Jenkins slave build node.
FROM ubuntu:15.10
MAINTAINER Fábio Tramasoli <fabio@tramasoli.com>

# Install and configure a basic SSH server
RUN apt-get update &&\
    apt-get install -y openssh-server &&\
    apt-get clean -y && rm -rf /var/lib/apt/lists/* &&\
    sed -i 's|session    required     pam_loginuid.so|session    optional     pam_loginuid.so|g' /etc/pam.d/sshd &&\
    mkdir -p /var/run/sshd
    
# Set user jenkins to the image
RUN adduser --quiet jenkins &&\
    echo "jenkins:jenkins" | chpasswd

# Install SCM and build tools
RUN apt-get update &&\
    apt-get install -y git subversion maven &&\
    apt-get clean -y && rm -rf /var/lib/apt/lists/*

# Standard SSH port
EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]