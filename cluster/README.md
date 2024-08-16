- ### step1 - Up virtual machine:
> vagrant up

- ### step2 - Testing:
> ansible all -m ping

- ### step3 - provision kubernetes master node:
> ansible-playbook playbook/common-playbook.yml

- ### step3 - provision kubernetes master node:
> ansible-playbook playbook/haproxy-playbook.yml

- ### step4 - provision kubernetes master node:
> ansible-playbook playbook/master-node-playbook.yml

- ### step5 - provision kubernetes master node:
> ansible-playbook playbook/worker-node-playbook.yml 

- ### node:
> inside the file: master-node-playbook.yml we have been deployed flannel-cni. please check it's up.
