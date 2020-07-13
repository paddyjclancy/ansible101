# -*- mode: ruby -*-
# vi: set ft=ruby :


# Install required plugins
required_plugins = ["vagrant-hostsupdater"]
required_plugins.each do |plugin|
    exec "vagrant plugin install #{plugin}" unless Vagrant.has_plugin? plugin
end

 

Vagrant.configure("2") do |config|
  config.vm.define "app" do |app|
    app.vm.box = "ubuntu/bionic64"
    app.vm.network "private_network", ip: "192.168.10.100"
    app.hostsupdater.aliases = ["development.app"]
    
    # sync folder
    app.vm.synced_folder "app", "/home/ubuntu/app"
    # Installing ansible 
    app.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "playbook.yml"
    end
  end
end