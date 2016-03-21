# -*- mode: ruby -*-
# vi: set ft=ruby :
$meta = <<SCRIPT
curl https://raw.githubusercontent.com/rapid7/metasploit-omnibus/master/config/templates/metasploit-framework-wrappers/msfupdate.erb > msfinstall && \
chmod 755 msfinstall && ./msfinstall
SCRIPT


Vagrant.configure(2) do |config|
#define FrontEnd
  config.vm.define "web" do |ubuntu|
    ubuntu.vm.hostname = "evbyminw1939Ubuntu"
    ubuntu.vm.box = "ubuntu/trusty64"
    ubuntu.vm.network "forwarded_port", guest: 80, host: 8080
    ubuntu.vm.box_check_update = true
    ubuntu.vm.synced_folder ".", "/vagrant", type: "virtualbox", disabled: false
    ubuntu.vm.provider "virtualbox" do |vb|
	vb.gui = false
   	vb.memory = "1024"
    end
    ubuntu.vm.provision "shell", inline: $meta
end

#define BackEnd
  config.vm.define "db" do |db|
    db.vm.hostname = "evbyminw1939debian"
    db.vm.box = "debian/jessie64"
    db.vm.network "forwarded_port", guest: 80, host: 8081
    db.vm.box_check_update = true
    db.vm.synced_folder ".", "/vagrant", type: "virtualbox", disabled: false
	db.vm.provider "virtualbox" do |vb|
	vb.gui = false
   	vb.memory = "1024"
  end
  db.vm.provision "chef_solo" do |chef|
    chef.add_recipe "mysql"
  end
  end
end
