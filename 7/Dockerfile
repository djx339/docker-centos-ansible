FROM centos:7
MAINTAINER Daniel D <djx339@gmail.com>
ENV container docker

# see https://hub.docker.com/_/centos/
RUN yum -y update; yum clean all; \
    (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == \
    systemd-tmpfiles-setup.service ] || rm -f $i; done); \
    rm -f /lib/systemd/system/multi-user.target.wants/*;\
    rm -f /etc/systemd/system/*.wants/*;\
    rm -f /lib/systemd/system/local-fs.target.wants/*; \
    rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
    rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
    rm -f /lib/systemd/system/basic.target.wants/*;\
    rm -f /lib/systemd/system/anaconda.target.wants/*;

RUN yum makecache fast \
    && yum -y install deltarpm epel-release initscripts \
    && yum -y update \
    && yum -y install \
            ansible \
            openssh-clients \
            openssh-server \
            python-pip \
            sudo \
            which \
    && yum clean all \
    && pip install jmespath \
    && systemctl enable sshd.service

# Install Ansible inventory file.
RUN echo -e '[local]\nlocalhost ansible_connection=local' > /etc/ansible/hosts

# Set default password for root
RUN echo 'root:docker.io' | chpasswd

# Add a tructed ssh key
RUN mkdir -p /root/.ssh/ \
    && curl -sLo /root/.ssh/authorized_keys https://raw.githubusercontent.com/djx339/docker-centos-ansible/master/ansible_docker.key.pub \
    && chmod 700 /root/.ssh \
    && chmod 640 /root/.ssh/authorized_keys

# we can has SSH
EXPOSE 22

VOLUME [ "/sys/fs/cgroup" ]
CMD ["/usr/sbin/init"]
