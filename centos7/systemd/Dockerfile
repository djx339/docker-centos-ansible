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
            sudo \
            which \   
    && yum clean all \
    && systemctl enable sshd.service

# Disable requiretty.
RUN sed -i -e 's/^\(Defaults\s*requiretty\)/#--- \1/'  /etc/sudoers

# Install Ansible inventory file.
RUN echo -e '[local]\nlocalhost ansible_connection=local' > /etc/ansible/hosts

RUN echo 'root:docker.io' | chpasswd

# we can has SSH
EXPOSE 22

VOLUME [ "/sys/fs/cgroup" ]
CMD ["/usr/sbin/init"]
