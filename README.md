# docker-centos-ansible [DEPRECATED]


## DEPRECATED

[AnsibleCheck](https://github.com/AnsibleCheck/ansiblecheck) is a better choice.

## Overview

[![Build Status](https://travis-ci.org/djx339/docker-centos-ansible.svg?branch=master)](https://travis-ci.org/djx339/docker-centos-ansible)

CentOS Docker image for Ansible playbook and role testing.

## Usage

```shell
# Host os is Ubuntu.
docker run --name ansible_centos7_systemd -itd --tmpfs /run -v /sys/fs/cgroup:/sys/fs/cgroup:ro djx339/centos-ansible:7

# Host os is non-Ubuntu
docker run --name ansible_centos7_systemd -itd -v /sys/fs/cgroup:/sys/fs/cgroup:ro djx339/centos-ansible:7-systemd
```
