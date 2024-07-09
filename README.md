INSTALL AND START NGINX USING THE ANSIBLE PLAYBOOK YAML FILE
****

Here, we are going to install and start the nginx service on the target servers by executing the playbook yaml file on the ansible configured machine. Please find the steps to do the same.

Prerequisite: Two ec2 instances with Ubuntu OS
You guys can clone my repo to try with my playbook YAML file

git clone https://github.com/surumivs/Ansible.git

1.	Configuring Ansible server and target server (Ec2 instances)
Ansible server: -
•	sudo apt update 
•	sudo apt install ansible
•	ssh-keygen (On both Ansible and target servers)
Copy the ‘id_rsa.pub’ from the ansible server and paste it on the ‘authorized_keys’ file on the target servers.
Now password less authentication is done, checking by
•	ssh <privateIPOf-Targetserver>

2.	Checking Ansible configuration working by Ansible ad-hoc commands
•	vi inventory (Add the Ips of target servers)
•	ansible -i inventory all -m “shell” -a “touch devopsclass”
This will create ‘devopsclass’ file in the target file

3.	Creating a playbook for installing & starting nginx

•	vi first-playbook.yml

---

- name: Installing and starting the nginx
  hosts: all
  become: true
  become_user: root

  tasks:
  - name: install nginx
    apt:
     name: nginx
     state: present
  - name: start nginx
    service:
     name: nginx
     state: started
![image](https://github.com/surumivs/Ansible/assets/170710844/6b559d88-cebc-4c64-8d86-9efe46074424)


4.	Run playbook
•	ansible-playbook -i inventory first-playbook.yml
![image](https://github.com/surumivs/Ansible/assets/170710844/ce9f37fd-598a-4906-bae1-13327e91287a)

It will gather, install, and start the nginx:

6.	Check on the target server that nginx is started
 ![image](https://github.com/surumivs/Ansible/assets/170710844/a2dc2102-baba-4a28-aba9-d3c027c039c2)



 


