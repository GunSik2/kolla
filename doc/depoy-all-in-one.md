
## Env
- EliteBook Intel i7, 16G Mem, 256G Disk
- CentOS 7.7
- wireless 1 network interface (wlo1)

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
