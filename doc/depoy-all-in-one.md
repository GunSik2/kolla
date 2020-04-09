
## Env
- EliteBook Intel i7, 16G Mem, 256G Disk
- CentOS 7.7
- wired 1 network interface (enp0s25)

## BRIDGE
- ifcfg-enp0s25 (original)
```
DEVICE=enp0s25
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
PREFIX=24
DEFROUTE=yes
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


## Test

## Reference
- https://docs.openstack.org/kolla-ansible/latest/user/quickstart.html
- https://github.com/openstack/kolla-ansible/releases
