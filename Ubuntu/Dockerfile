FROM ubuntu:16.04

ARG USER=creative

RUN apt-get update -y && \
    apt-get -y install openssh-server

RUN useradd $USER && \
    echo "creative:creative123" | chpasswd && \
    usermod -s /bin/bash $USER && \
    mkdir -p /home/$USER/.ssh/ && \
    chmod 700 /home/$USER/.ssh && \
    mkdir -p /var/run/sshd

COPY creative.pub /tmp/$USER.pub

RUN cat /tmp/$USER.pub > /home/$USER/.ssh/authorized_keys

RUN chown $USER:$USER -R /home/$USER/.ssh && \
    chmod 600 /home/$USER/.ssh/authorized_keys

#RUN apt-get -y install ansible

RUN mkdir -p /home/$USER/.ansible/tmp/ && \
    chown $USER:$USER -R /home/$USER/.ansible/    

RUN apt-get -y install sudo && \
    apt-get -y install openjdk-8-jre

RUN echo "$USER ALL=NOPASSWD: ALL" >> /etc/sudoers

CMD ["/usr/sbin/sshd", "-D"]
