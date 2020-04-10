
## Env
- EliteBook Intel i7, 16G Mem, 256G Disk
- CentOS 7.7
- wired 1 network interface (enp0s25)

## BRIDGE
![Architecture](https://user-images.githubusercontent.com/11453229/78886356-03c44200-7a99-11ea-8820-01dbce8cc4db.png)

- cd /etc/sysconfig/network-scripts/
- ifcfg-enp0s25 (original)
```
DEVICE=enp0s25
NAME=enp0s25
TYPE=Ethernet
BOOTPROTO=dhcp
DEFROUTE=yes
ONBOOT=no
```
- ifcfg-enp0s25 
```
DEVICE=enp0s25
TYPE=Ethernet
BOOTPROTO=none
ONBOOT=yes
```
- ifcfg-enp0s25.10 : public for access
```
DEVICE=enp0s25.10
TYPE=Ethernet
BOOTPROTO=none
ONBOOT=yes
VLAN=yes
IPADDR=10.0.5.201
GATEWAY=10.0.5.1
PREFIX=24
```
- ifcfg-enp0s25.101 : unnumbered for api 
```
DEVICE=enp0s25.101
TYPE=Ethernet
BOOTPROTO=none
ONBOOT=yes
VLAN=yes
```

## Installation
- Install Python build dependencies
```
sudo yum install python-devel libffi-devel gcc openssl-devel libselinux-python
```
- Install dependencies using a virtual environment
```
sudo yum install python-virtualenv
virtualenv kolla-env
source kolla-env/bin/activate
(kolla-env) pip install -U pip
(kolla-env) pip install ansible
```
- Configure
```
# grep -v "^#" /etc/kolla/globals.yml | egrep -v "^$"
---
kolla_base_distro: "centos"
kolla_install_type: "binary"
openstack_release: "train"
nova_compute_virt_type: "kvm"
kolla_internal_vip_address: "10.0.5.202" 
network_interface: "enp0s25.10"
neutron_external_interface: "enp0s25.101"
```
- Deployment
```
(kolla-env) kolla-ansible -i ./all-in-one bootstrap-servers
(kolla-env) kolla-ansible -i ./all-in-one prechecks
(kolla-env) kolla-ansible -i ./all-in-one deploy

```

## Test
- Install openstack cli & create credentials
```
(kolla-env) pip install python-openstackclient
(kolla-env) kolla-ansible post-deploy
(kolla-env) . /etc/kolla/admin-openrc.sh
```
- Create sample image and network
```
(kolla-env) /usr/share/kolla-ansible/init-runonce
```
## Reference
- https://docs.openstack.org/kolla-ansible/latest/user/quickstart.html
- https://github.com/openstack/kolla-ansible/releases
- https://www.linuxtechi.com/vlan-tagged-nic-ethernet-card-centos-rhel-servers/
