k8s-cluster-deploy Role
=========

This ansible role deploy one-master Kubernetes cluster with Docker runtime on apt based linux.
(deploy Cri-O as run time currently in development)

Requirements
------------

- apt based linux (fully checked on debian 10)
- All kinds of firewall down

Inventory File
--------------

One master and as many nodes as you wish.

NOTICE
- Place the master host first in the list, and after thet all the nodes.
- ansible_host varible must contain user with sudo permission.

* Example:
```
---
[kubernetes]
192.168.64.9 ansible_user=k8sadmin #master
192.168.64.7 ansible_user=k8sadmin #node1
192.168.64.8 ansible_user=k8sadmin #node2
```

Role Variables
--------------

vars/main.yml:
```
- reinstall: false
Default value for reinstall is false.
If user tried in the past to install kubernetes with kubeadm he should override this value to true in playbook.

ONLY FOR Cri-O (not needed for docker)
- OS
the name of the operating system you use and version of it in upper case letters.
- VERSION
version of crio you whould like to install.
```

Example Playbook
----------------

playbook.yml:
```
---
- name: install kubernetes
  hosts: kubernetes
  become: true
  roles:
  - role: kubernetes
    uninstall: true #Default is false.
```
License
-------

Open Source

Author Information
------------------

Developed by Ron Megini.
For question: ronmegini34350@gmail.com
