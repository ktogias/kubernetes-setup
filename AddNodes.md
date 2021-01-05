ssh-copy-id root@<new-node-ip>
Add new nodes at hosts file in groups kuball, kubworkers, kubpublic (if they can have a public ip) and create newkubnodes group that contans only the new nodes
ansible-playbook setup-hosts.yaml --limit newkubnodes
change new nodes ips in ansible hosts file to match given public ip
ssh root@<new-node-ip>
ansible newkubnodes -a "reboot "
ansible-playbook test-hosts-networking.yaml
ansible-playbook setup-kuberentes.yaml --limit newkubnodes
ansible newkubnodes -a "reboot "