# Kubernetes cluster provided by Vagrant & Ansible

Run a Kubernetes cluster locally using Vagrant and Ansible.

This will create and setup one Kubernetes master and $NodeCount number of nodes. 
'NodeCount' can be changed inside Vagrantfile to define number of nodes. Default is 3.

* manager - 192.168.100.10
* node 1 - 192.168.100.11
* node 2 - 192.168.100.12
* node 3 - 192.168.100.13

# Requirements

Install [Vagrant][vagranthome] on your machine.

# Setup

## Boot Vagrant machines

```
$ git clone https://github.com/dobby-dobster/kubernetes-vagrant-ansible.git
$ cd kubernetes-vagrant-ansible
vagrant up
```

## Connect to master or nodes

```
vagrant ssh <master|node1>
```

To destroy the environment:

```
vagrant destroy
```

[vagranthome]: https://www.vagrantup.com/docs/installation/  "Vagrant installation