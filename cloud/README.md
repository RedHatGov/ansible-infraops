# build-a-cloud

This repository contains a set of Ansible playbooks that set up VPCs (or their equivalents)
in AWS, Azure, and OpenStack.  In addition, it connects them together using a DMVPN overlay
using a Cisco Cloud Services Router 1000v.

## Pre-requisites:

### Install PIP on Centos 7:
```
yum install epel-release
yum install python-devel python-pip
```

### Install OpenStack Clients:
```
yum groupinstall development
pip install python-openstackclient
pip install 'setuptools>=11.3'
pip install shade
```

### Install EC2 Clients:
```
pip install awscli
```

### Install Ansible:
```
yum -y install libffi-devel openssl-devel
pip install git+git://github.com/ansible/ansible.git@stable-2.1
```

### Install Azure API/CLI:
```
pip install --no-cache-dir --upgrade 'azure==2.0.0rc5'
yum -y install npm
npm install azure-cli -g
```

## Proceedure:

1) Create a hosts file (named "hosts") in the working directory:
```
[hubs]
[spokes]
[hosts]
```

2) Update "cloud_vars.yml" with regions, amis, ssh-keys, etc.

### Running the Playbooks:

```
ansible-playbook build_aws_vpc.yml

ansible-playbook -i hosts configure_csrs.yml

ansible-playbook -i hosts destroy_aws_vpc.yml
```