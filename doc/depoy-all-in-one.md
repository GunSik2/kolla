
## Env
- EliteBook Intel i7, 16G Mem, 256G Disk
- CentOS 7.7
- wired 1 network interface (enp0s25)

## BRIDGE
- Diagram
![Architecture](https://user-images.githubusercontent.com/11453229/78886356-03c44200-7a99-11ea-8820-01dbce8cc4db.png)

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
pip install -U pip
pip install ansible
```
- Configure
```

```
- Deployment
```
kolla-ansible -i ./all-in-one bootstrap-servers
kolla-ansible -i ./all-in-one prechecks
kolla-ansible -i ./all-in-one deploy

```

## Test

## Reference
- https://docs.openstack.org/kolla-ansible/latest/user/quickstart.html
- https://github.com/openstack/kolla-ansible/releases
- https://www.linuxtechi.com/vlan-tagged-nic-ethernet-card-centos-rhel-servers/
