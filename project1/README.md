Ansible Project 1
==================

Infrastructure Setup
--------------------
- 1 x management instance (ansible)
- 2 x managed instances (server1 & server2)

```shell
# make sure you're in root directory of the repository
git pull
vagrant up
vagrant status
```

Ansible tasks
--------------
Switch to directory **project1**
1. Create inventory and include servers into group **web**
2. Create playbook which contains 3 tasks (see below for details) and playbook will deploy to group **web**
3. include task to create users (https://docs.ansible.com/ansible/latest/collections/ansible/builtin/user_module.html):
	- **david** with uid **4467** and home directory **/home/david_home** on **server1**
	- **john** with secondary group **wheel** on both servers
4. include task to ensure the following packages exist (https://docs.ansible.com/ansible/latest/collections/ansible/builtin/yum_module.html or https://docs.ansible.com/ansible/latest/collections/ansible/builtin/package_module.html):
	- **vim** on **server2**
	- **unzip** and **bind-utils** on both servers
	- **httpd** on **server1**
5. include task to ensure **firewalld** is disabled and not running (https://docs.ansible.com/ansible/latest/collections/ansible/builtin/systemd_module.html or https://docs.ansible.com/ansible/latest/collections/ansible/builtin/service_module.html) on any of the servers

Ansible deployment
------------------
```shell
# make sure you're in root directory of the repository
vagrant ssh
# inside ansible vm change to project1 directory where projects inventory and playbooks are
cd /vagrant/project1
# run ansible-playbook with your playbook(s)
```
