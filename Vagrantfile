# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "bento/centos-6.7"

  config.vm.provider "parallels" do |v|
      v.memory = 1024
      v.cpus = 2
      v.use_linked_clone = true
      v.customize ["set", :id, "--sh-app-guest-to-host", "off"]
      v.customize ["set", :id, "--shared-cloud", "off"]
      v.customize ["set", :id, "--shared-profile", "off"]
      v.update_guest_tools = false
  end
  config.vm.provision "shell", inline: <<-SHELL
     sudo yum update -y
  SHELL
  config.vm.provision "chef_zero" do |chef|
    chef.install = true
    chef.cookbooks_path = ["cookbooks", "site-cookbooks"]
    chef.roles_path = "roles"
    chef.nodes_path = "nodes"
    chef.data_bags_path = "data_bags"
    chef.add_role("java")
    chef.add_role("jboss")
    #chef.log_level = 'debug'
  end
end
