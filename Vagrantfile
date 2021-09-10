vagrantfile_api_version = "2"
# Project Name (VirtualBox Group Name)
vb_group_name = "/ansible"
# Project description
project_description = "Ansible Playground"
# Default system resources
default_os = "centos/7"
default_cpus = "1"
default_mem = "512"
default_boot = "disk"
domain = "local"


##################
# VM parameters
##################
boxes = [
  { :name => :ansible, :role => 'mgt',  :os => default_os,  :ip => "10.0.13.151", :cpus => default_cpus, :mem => 1024,  :primary => true,   :autostart => true },
  { :name => :server1, :role => 'client',  :os => default_os, :ip => "10.0.13.152", :cpus => default_cpus, :mem => default_mem,  :primary => false,   :autostart => true },
  { :name => :server2, :role => 'client',  :os => default_os, :ip => "10.0.13.153", :cpus => 1, :mem => default_mem,  :primary => false,   :autostart => true },
]

####################
# Install scripts
####################
$default = <<INSTALL
  echo -e "==> Standard CentOS configuration bootstraping\n"
  setenforce 0
  sed -i 's/^SELINUX=.*/SELINUX=disabled/g' /etc/selinux/config
  yum install -y epel-release
INSTALL

Vagrant.configure(vagrantfile_api_version) do |config|

#####################################################
# Default configuration settings (VM provisioning)
#####################################################

  vm_default = proc do |vb|
    vb.vm.boot_timeout = 90
    vb.ssh.insert_key = false
    vb.vbguest.auto_update = true
    vb.vbguest.installer_options = { allow_kernel_upgrade: true, reboot_timeout: 5000 }
  end

#########################################################
# VM configuration settings per role (VM provisioning)
#########################################################

  boxes.each do |opts|
    config.vm.define opts[:name], primary: opts[:primary], autostart: opts[:autostart] do |config|
      vm_default.call(config)
      config.vm.box = default_os
      config.vm.provider :virtualbox do |vb|
        vb.name = "%s" % opts[:name].to_s
        vb.gui = false
        vb.customize [
          "modifyvm", :id,
          "--memory", opts[:mem],
          "--cpus", opts[:cpus],
          "--boot1", default_boot,
          "--vram", "8",
          "--audio", "none",
          "--groups", vb_group_name,
          "--description", project_description
        ]
      end
      config.vm.host_name = "%s.#{domain}" % opts[:name].to_s
      config.vm.network :private_network, ip: opts[:ip]
      config.vbguest.auto_update = false
      config.vm.provision "shell", inline: $default
      if opts[:role] == 'mgt'
        config.vm.synced_folder ".", "/vagrant", disabled: false, type: "rsync", rsync__args: ['--verbose', '--archive', '--delete', '-z'] , rsync__exclude: ['.git','venv']
        config.vm.provision "file", source: "~/.vagrant.d/insecure_private_key", destination: "/home/vagrant/.ssh/id_rsa"
      end
    end
  end
end
