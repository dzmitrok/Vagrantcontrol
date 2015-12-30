# -*- mode: ruby -*-
# vi: set ft=ruby :



Vagrant.configure(2) do |config|
#define FrontEnd
  config.vm.define "web" do |web|
    web.vm.hostname = "evbyminw1939web"
    web.vm.box = "centos/7"
    web.vm.network "forwarded_port", guest: 80, host: 8080
    web.vm.synced_folder ".", "/home/vagrant/sync", disabled: true
    web.vm.provision "chef_solo" do |chef|
    	chef.cookbooks_path = "chef-repo"
	    chef.add_recipe "apache2"
    end
  end
#define BackEnd
  config.vm.define "db" do |db|
    db.vm.hostname = "evbyminw1939db"
    db.vm.box = "debian/jessie64"
    db.vm.network "forwarded_port", guest: 3306, host: 3306
    db.vm.provision "chef_solo" do |chef|
    	chef.cookbooks_path = "chef-repo"
	    chef.add_recipe "mysql"
    end
  end
end
