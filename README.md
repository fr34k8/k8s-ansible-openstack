k8s-on-openstack
================

This is a modified version of [infraly/k8s-on-openstack](https://github.com/infraly/k8s-on-openstack). In contrast to the previous playblook, this modified version 

- does **NOT** use a Kubernetes' OpenStack cloud provider but
- does deploy Kubernetes on an OpenStack cluster using Ansible and with kube-router.

It is based on the following tools:

  - [kubeadm](https://github.com/kubernetes/kubeadm)
  - [Ansible](https://github.com/ansible/ansible)
  - [kube-router](https://github.com/cloudnativelabs/kube-router)

Prerequisites
-------------

- [Ansible](https://github.com/ansible/ansible) (tested with version 2.4)
- [Shade](https://pypi.python.org/pypi/shade) library required by Ansible OpenStack modules (`python-shade` for Debian, `pip install shade` otherwise)

Getting started
---------------

The following mandatory environment variables need to be set before calling `ansible-playbook`:

  - `OS_*`: standard OpenStack environment variables such as `OS_AUTH_URL`, `OS_USERNAME`, ...
  - `KEY`: name of an existing SSH keypair

The following optional environment variables can also be set:

  - `NAME`: name of the Kubernetes cluster, used to derive instance names, `kubectl` configuration and security group name
  - `IMAGE`: name of an existing Ubuntu 16.04 image
  - `NETWORK`: name of the network to which instances should be connected
  - `EXTERNAL_NETWORK`: name of the neutron external network, defaults to 'public'
  - `FLOATING_IP_POOL`: name of the floating IP pool
  - `FLOATING_IP_NETWORK_UUID`: uuid of the floating IP network (required for LBaaSv2)
  - `NODE_MEMORY`: how many MB of memory should nodes have, defaults to 4GB
  - `NODE_COUNT`: how many nodes should we provision, defaults to 3
  - `MASTER_BOOT_FROM_VOLUME`: boot the master instance on a volume for data persistence, defaults to True
  - `MASTER_TERMINATE_VOLUME`: delete the volume when master instance is destroy, defaults to True
  - `MASTER_VOLUME_SIZE`: size of the master volume
  - `MASTER_MEMORY`: how many MB of memory should master have, defaults to 4 GB

Spin up a new cluster:

```console
ansible-playbook site.yaml
```

Destroy the cluster:

```console
ansible-playbook destroy.yaml
```

Authors
------

- Original Authors of [infraly/k8s-on-openstack](https://github.com/infraly/k8s-on-openstack):
  - François Deppierraz <francois.deppierraz@infraly.ch>
  - Oli Schacher <oli.schacher@switch.ch>
  - Saverio Proto <saverio.proto@switch.ch>
- Author of [this modified version](https://github.com/pfisterer/k8s-ansible-openstack-kube-router)
  - [Dennis Pfisterer](http://www.dennis-pfisterer.de)
