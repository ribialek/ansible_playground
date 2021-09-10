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
3. task to create users (https://docs.ansible.com/ansible/latest/collections/ansible/builtin/user_module.html):
	- **david** with uid **4467** and home directory **/home/david_home** one server1
	- **john** with secondary group **wheel** one both servers
