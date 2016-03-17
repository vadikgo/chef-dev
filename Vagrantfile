# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "boxcutter/ol67"

  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.memory = "512"
    vb.gui = false
    vb.linked_clone = true
  end

  config.vm.provider "parallels" do |prl|
    prl.memory = "512"
    prl.linked_clone = true
    prl.update_guest_tools = false
    prl.check_guest_tools = false
    prl.customize ["set", :id, "--sh-app-guest-to-host", "off"]
    prl.customize ["set", :id, "--shared-cloud", "off"]
    prl.customize ["set", :id, "--shared-profile", "off"]
    prl.customize ["set", :id, "--time-sync", "on"]
  end

  config.vm.provision "chef_zero" do |chef|
    chef.install = true
    chef.cookbooks_path = ["cookbooks", "site-cookbooks"]
    chef.roles_path = "roles"
    chef.nodes_path = "nodes"
    chef.data_bags_path = "data_bags"
    #chef.log_level = 'debug'
    #chef.arguments = "-u jboss2"
  end
end
