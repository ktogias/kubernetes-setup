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
  vim <your_hosts_file>
  
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

[initkubmaster]
ip1

[kub-workers]
ip2
ip3
ip4
ip5
....
 ```
        
### Create your vars file
  cp vars.dist <your_vars_file>
and edit

### Run playbook

ansible-playbook -i <your_hosts_file> -e @<your_vars_file> playbook/<playbook>.yaml
