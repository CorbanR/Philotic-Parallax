# -*- mode: ruby -*-
# vi: set ft=ruby :
#
#VirtualBox Specific
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"

  config.vm.network "forwarded_port", guest: 22, host: 2222, id: "ssh"
config.vm.provider "vmware_fusion" do |v, override|
  override.vm.box = "precise64_fusion"
  override.vm.box_url = "http://files.vagrantup.com/precise64_vmware.box"
  override.vm.network "forwarded_port", guest: 22, host: 2222, id: "ssh"
  override.vm.network "forwarded_port", guest: 80, host: 8080, id: "http"
  v.vmx["memsize"] = "1024"
  v.vmx["numvcpus"] = "2"

#Ansible Specific 
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "vagrant.yml"
    ansible.inventory_path = "inventories/vagrant"
    ansible.verbose = "v"
   end
  end
end
