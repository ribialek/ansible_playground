Ansible Playground
==================

Requirements
------------
```shell
# Install VBox and vagrant
brew install --cask virtualbox-extension-pack virtualbox vagrant
# It will require restart and allowing Oracle software to interact with system (Privacy & Security I believe)
# Install vagrant plugins
vagrant plugin install vagrant-vbguest vagrant-hostmanager
# And download vagrant box
vagrant box add centos/7
vagrant box add ubuntu/focal64
```
Each project has its own infrastructure managed by vagrant. To avoid conflicts (nfs share errors) destroy vagrant infrastructure in project that was completed

- [project1](./project1/README.md)
- [project2](./project2/README.md)
