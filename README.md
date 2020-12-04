## Setting up a kubernetes cluster

### Create 5 vms and install minimal centos8

### Copy your ssh key to each node to be able to ssh with no password
```
  ssh-copy-id root@ip1
  ssh-copy-id root@ip2
  ssh-copy-id root@ip3
  ssh-copy-id root@ip4
  ssh-copy-id root@ip5
```

### Install ansible to a pc to manage the cluster nodes
  yum install ansible
  vim /etc/ansible/hosts
  
  Add thew following:
  ```
[kub-all]
ip1
ip2
ip3
ip4
ip5
...

[kub-masters]
ip1

[kub-workers]
ip2
ip3
ip4
ip5
....
 ```
        
### Install python3 on each node as it is requried for ansible

Ssh on each node and run
  dnf install -y python3 && ln -s /usr/bin/python3 /usr/bin/python
  
### Update nodes

Run
  ansible kubernetes -a "dnf upgrade --refresh -y " -u root
  
### Reboot nodes

Run
  ansible kubernetes -a "reboot " -u root
  
Dont be afraid of ansible error message. It just lost each node after issuing the reboot command.

### Disable selinux

Run 
  ansible kubernetes -a "setenforce 0 " -u root
  ansible kubernetes -a "sed -i --follow-symlinks 's/SELINUX=enforcing/SELINUX=disabled/g' /etc/sysconfig/selinux " -u root
  
### Enable IP masquerade at the firewall

Run 
  ansible kubernetes -a "firewall-cmd --add-masquerade --permanent " -u root


