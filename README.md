Ansible Playground
==================

Overview
---------
- each project has its own infrastructure managed by vagrant.
- vagrant infrastructure to be destroyed when project completed.<br />
  **NOTE:** destroy infrastructure to avoid conflicts (nfs share errors).<br />
- create your own branch `<github_username>_<project>` (e.g. `NMankrado_project1`) before starting working with project.<br />
  **NOTE:** do not merge your branch with master branch.<br />

Requirements
------------
```shell
# Install VBox and vagrant
# mac users with use of brew package manager
brew install --cask virtualbox-extension-pack virtualbox vagrant
# windows users with use of chocolatey package manager
cinst -y virtualbox virtualbox-guest-additions-guest.install vagrant
# It will require restart and allowing Oracle software to interact with system (on mac Privacy & Security I believe)
# Install vagrant plugins
vagrant plugin install vagrant-vbguest vagrant-hostmanager
# And download vagrant box
vagrant box add centos/7
vagrant box add ubuntu/focal64
```

Projects
---------
[project1](./project1/README.md)<br />
&emsp;==> ansible install and configuration<br />
&emsp;==> inventory<br />
&emsp;==> basic playbooks with variables<br />
&emsp;==> variable precedence rules<br />

[project2](./project2/README.md)<br />
&emsp;==> ansible roles<br />
&emsp;==> running tasks conditionally<br />
&emsp;==> use system facts as register variables<br />
