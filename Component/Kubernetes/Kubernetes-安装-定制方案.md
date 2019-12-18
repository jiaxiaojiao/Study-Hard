## Kubernetes 定制方案

定制方案 需要花费更多的精力，但是覆盖了从零开始搭建Kubernetes集群的通用建议到分步骤的细节指引。

### 目录
* [云服务商和云操作系统支持的方案](#云服务商和云操作系统支持的方案)
* [私有虚拟机支持的方案](#私有虚拟机支持的方案)
* [裸机支持的方案](#裸机支持的方案)
* [集成方案](#集成方案)


### 云服务商和云操作系统支持的方案
* AWS + coreos
* GCE + CoreOS
* AWS + Ubuntu
* Joyent + Ubuntu
* Rackspace + CoreOS

### 私有虚拟机支持的方案
* Vagrant（采用CoreOS和flannel）
* CloudStack（采用Ansible，CoreOS和flannel）
* Vmware（采用Debian）
* juju.md（采用Juju，Ubuntu和flannel）
* Vmware（采用CoreOS和flannel）
* libvirt-coreos.md（采用CoreO）
* oVirt
* libvirt（采用Fedora和flannel）
* KVM（采用Fedora和flannel）

### 裸机支持的方案
* Offline（无需互联网，采用CoreOS和flannel）
* fedora/fedora_ansible_config.md
* Fedora单节点
* Fedora多节点
* Centos
* Ubuntu
* Docker多节点

### 集成方案
Kubernetes on Mesos（采用GCE）


