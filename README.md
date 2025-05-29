# Ansible-practice
What is Ansible?

Ansible is an open-source automation tool used for:
Configuration Management: Automatically setting up and maintaining systems (e.g., installing packages, editing config files).

Application Deployment: Deploying apps across multiple servers.

Orchestration: Coordinating multiple machines together (e.g., setting up a multi-tier web application).

Provisioning: Setting up infrastructure (e.g., launching cloud instances).

Security and Compliance: Automating security policies and updates.

It uses simple YAML syntax in files called playbooks, making it readable and easy to write.

Example Use Case
You want to install Apache on 50 servers. Instead of logging in to each server and running commands, you can write one Ansible playbook and run it once — and all servers get configured.


goto google search install ansible in ubuntu  //OR
https://docs.ansible.com/ansible/latest/installation_guide/installation_distros.html

# add repository of ansible add-apt-repository --yes --update ppa:ansible/ansible
# apt-get apdate 
# apt-get install ansible -y 

# send private key on server :/home/ubuntu/virginia-key.pem


# vim /etc/ansible/hosts
# 172.31.83.128 ansible_user=ubuntu ansible_ssh_private_key_file=/home/ubuntu/virginia-key.pem
OR 
# Ex 2: A collection of hosts belonging to the 'webservers' group:

## [webservers]
## alpha.example.org
## beta.example.org
## 192.168.1.100
## 192.168.1.110
[servers]
server_1 ansible_host=44.203.5.106
server_2 ansible_host=13.217.162.186

[servers:vars]
ansible_python_interpreter=/usr/bin/python3
ansible_user=ubuntu
ansible_ssh_private_key_file=/home/ubuntu/virginia-key.pem

# ansible servers -m ping

# ansible all -m ping (ping all grps) 
# ansible all -m ping -u ubuntu (ping perticular user)

# ansible servers -a "free -h" (check ram in grp servers)

# Now supose we have multiple groups and I want run command at all groups modify some configuration in  /etc/ansible/hosts
# grp-1
[servers]
server_1 ansible_host=44.203.5.106
# grp-2
[prd]
server_2 ansible_host=13.217.162.186

[all:vars]
ansible_python_interpreter=/usr/bin/python3
ansible_user=ubuntu
ansible_ssh_private_key_file=/home/ubuntu/virginia-key.pem

# ansible servers -m ping
# ansible prd -m ping
# ansible-inventory --list


✅ What is an Ansible Playbook?
An Ansible playbook is a YAML file that defines a set of instructions to automate tasks on remote systems.

🛠️ It’s like a script that tells Ansible what to do, where to do it, and how to do it.

# Install nginx 
mkdir playbook 
vim install_nginx.yml
-
  name: Install Nginx and start it
  hosts: servers
  become: yes
  tasks:
   - name: Install Nginx
     apt:
      name: nginx
      state: latest
      update_cache: yes
   - name: Start Nginx
     service:
      name: nginx
      state: started
      enabled: yes
~
# run command
ansible-playbook install_nginx.yml

# diffrent grp install & host website

-
  name: Install nginx and host static website
  hosts: prd
  become: yes
  tasks:
   - name: Install nginx
     apt:
      name: nginx
      state: latest
      update_cache: yes

   - name: Start nginx
     service:
       name: nginx
       state: started
       enabled: yes

   - name: Deploy web page
     copy:
       src: /home/ubuntu/index.html
       dest: /var/www/html/index.html
