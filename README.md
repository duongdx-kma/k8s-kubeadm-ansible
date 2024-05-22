- ##### Up virtual machine:
> vagrant up

- ##### Testing:
> ansible all -m ping

- ##### provision NFS server:
> ansible-playbook playbook/nfs-server-playbook.yml

- ##### provision kubernetes master node:
> ansible-playbook playbook/master-node-playbook.yml 

- ##### provision kubernetes master node:
> ansible-playbook playbook/worker-node-playbook.yml 

- #### node:
> inside the file: master-node-playbook.yml we have been deployed flannel-cni. please check it's up.
