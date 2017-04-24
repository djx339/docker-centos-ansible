# docker-centos-ansible
CentOS Docker image for Ansible playbook and role testing.


## Usage

```shell
# Host os is Ubuntu.
docker run --name ansible_centos7_systemd -v /tmp/$(mktemp -d):/run -itd -v /sys/fs/cgroup:/sys/fs/cgroup:ro djx339/centos-ansible:7-systemd

# Host os is not Ubuntu
docker run --name ansible_centos7_systemd -itd -v /sys/fs/cgroup:/sys/fs/cgroup:ro djx339/centos-ansible:7-systemd
```
