 # -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # Base VM OS configuration.
  config.vm.box = "geerlingguy/centos6"
  config.ssh.insert_key = false
  config.vm.synced_folder '.', '/vagrant', disabled: true

  # General VirtualBox VM configuration.
  config.vm.provider :virtualbox do |v|
    v.memory = 512
    v.cpus = 1
    v.linked_clone = true
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--ioapic", "on"]
  end

  # Ansible Controller
  config.vm.define "acs" do |acs|
    acs.vm.hostname = "acs"
    acs.vm.network :private_network, ip: "192.168.1.2"
  end

  # Apache.
  config.vm.define "web" do |web|
    web.vm.hostname = "web"
    web.vm.network :private_network, ip: "192.168.1.3"

    web.vm.provision "shell",
      inline: "sudo yum update -y"

    web.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--memory", 256]
    end
  end

  # MySQL.
  config.vm.define "db" do |db|
    db.vm.hostname = "db"
    db.vm.network :private_network, ip: "192.168.1.4"
  end
end