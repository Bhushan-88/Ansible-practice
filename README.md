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

# send private key on server 
# vim /etc/ansible/hosts
# 172.31.83.128 ansible_user=ubuntu ansible_ssh_private_key_file=/home/ubuntu/virginia-key.pem
# ansible all -m ping

# ansible server-1 -m ping
