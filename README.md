# WordPress+Nginx+PHP-FPM+PerconaDB Deployment

### Introduction
---
This repo contains 5 roles for ansible:

- nginx - install and configure nginx to serve static files and pass requests to php-fpm
- nginx_proxy - install and configure nginx as load balancer
- percona - install and configure PerconaDB
- php5-fpm - install and configure php-fpm
- wordpress - install and configure wordpress

### Requirements
---
- Linux host
- Ansible 2.0 or newer
- Vagrant 1.8
- VirtualBox 5.14 or newer

### Installation
---
Clone this repo
```sh
$ cd repo
$ vagrant up
$ firefox localhost:8037
```
By default vagrant will start 4 VMs and provision them with ansible.

After provisioning You will get:

- One VM with nginx as proxy
- Two VMs with nginx+php-fpm+wordpress(php version 7, can be changed in config)
- One VM with PerconaDB

To test availability when one app server down use command:

```
$ vagrant halt machine2
```

### Configuration
---

If You want to change ip addresses of VMs, You need to change them in Vagrantfile:

```
machine.vm.network "private_network", ip: "192.168.33.#{9+machine_id}"
```

in ansible inventory file(hosts)

```
[db]
machine1 ansible_ssh_host=192.168.33.10 ansible_ssh_private_key_file=./.vagrant/machines/machine1/virtualbox/private_key
[app]
machine2 ansible_ssh_host=192.168.33.11 ansible_ssh_private_key_file=./.vagrant/machines/machine2/virtualbox/private_key
machine3 ansible_ssh_host=192.168.33.12 ansible_ssh_private_key_file=./.vagrant/machines/machine3/virtualbox/private_key
[web]
machine4 ansible_ssh_host=192.168.33.13 ansible_ssh_private_key_file=./.vagrant/machines/machine4/virtualbox/private_key
```
and in ```nginx_proxy/defaults/main.yml```


### TODO
---
- [ ] Make dynamic inventory for ansible
- [ ] Fix problem with vagrant keys

### Licensing
---
Please see the file called LICENSE.

### Author Information
---
This roles was created by Petr Enkov(peter@mail.ru).
