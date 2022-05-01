Ansible Project 1
==================

Infrastructure Setup
--------------------
- 1 x management instance (ansible)
- 2 x managed instances (centos & ubuntu)

```shell
# make sure you're in root directory of the repository
git pull && cd project2
vagrant up
vagrant status
# accessing instances
vagrant ssh # to access ansible management instance
vagrant ssh centos # to access centos client instance
vagrant ssh ubuntu # to access ubuntu client instance
```

Ansible tasks
--------------
Switch to directory **project2** if not already there
1. Create directory structure which include placeholder for roles, playbooks and inventory
2. Update ansible.cfg configuration used by the project2 with options for location of the inventory and roles (https://docs.ansible.com/ansible/latest/installation_guide/intro_configuration.html)
3. using ansible-galaxy (https://galaxy.ansible.com/docs/contributing/creating_role.html) create the following roles (make sure created roles are in correct path):
	- **users** -> role used for user/group management
	- **packages** -> role used for software management
	- **services** -> role used for services management
4. Create task in role **users**:
	- task to generate users with option to specify 'uid' if required using the following variable (see code below)
	- user resources to be deployed to all managed  systems
	```shell
	# make sure you're in root directory of the repository
	ssh_users:
		- name: "user1"
			uid: 1006
			groups: ["nfsnobody"]
		- name: "user2"
			groups: ["nfsnobody"]
		- name: "user3"
			uid: 1007
	```
	HINTS:
	- use two tasks executed conditionally based on required parameter (user's 'uid')
	- cleanup role from unused subfolders (good practice)
5. Create task in role **packages**:
	- "httpd" -> to be installed on all supported
	- "vim" -> to be installed on all
	HINTS:
	- httpd package is only supported on RedHat/CentOS, maybe 'ansible_facts.os_family' could be used to set condition where package is deployed
6. Create task in role **services**:
	- check if 'postfix' is running
	- stop and disable 'postfix' only if postfix is running
	HINTS:
	- use register to catch output of running services as variable
	- use condition with registered variable to determine if disabling service task should run

Ansible deployment
------------------
```shell
# make sure you're in root directory of the repository
vagrant ssh
# inside ansible vm change to project1 directory where projects inventory and playbooks are
cd /vagrant/project2
# run ansible-playbook with your playbook(s)
```
