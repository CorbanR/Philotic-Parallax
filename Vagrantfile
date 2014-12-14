# -*- mode: ruby -*-
# vi: set ft=ruby :
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.synced_folder ".", "/vagrant", disabled: true
    config.vm.provider :virtualbox do |vb, override|
      vb.customize ["modifyvm", :id, "--memory", "512"]
      vb.customize ["modifyvm", :id, "--cpus", "1"]
  end
    config.vm.provider "vmware_fusion" do |vm, override|
      override.vm.box = "CorbanRaun/trusty64"
      vm.vmx["memsize"] = "512"
      vm.vmx["numvcpus"] = "2"
  end
  config.vm.define "philotic" do |philotic|
    philotic.vm.hostname = "philotic-vagrant"
    philotic.vm.network "private_network", ip: "192.168.50.2"
    philotic.vm.network "forwarded_port", guest: 80, host: 8080, id: "http"
    philotic.vm.provision "ansible" do |ansible|
      ansible.limit = 'all'
      ansible.playbook = ".vagrant.yml"
    end
  end
end
