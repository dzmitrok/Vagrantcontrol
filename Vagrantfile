# -*- mode: ruby -*-
# vi: set ft=ruby :
#install metasploit-framework
$meta = <<SCRIPT
curl https://raw.githubusercontent.com/rapid7/metasploit-omnibus/master/config/templates/metasploit-framework-wrappers/msfupdate.erb > msfinstall && \
chmod 755 msfinstall && ./msfinstall
SCRIPT
# linux kernel headers and the basic developer tools
$KerDev = <<SCRIPT
sudo apt-get install xorg gnome-core -y
#sudo apt-get install linux-headers-$(uname -r) build-essential dkms
#wget http://download.virtualbox.org/virtualbox/5.0.16/VBoxGuestAdditions_5.0.16.iso
#sudo mkdir /media/VBoxGuestAdditions
#sudo mount -o loop,ro VBoxGuestAdditions_5.0.16.iso /media/VBoxGuestAdditions
#sudo sh /media/VBoxGuestAdditions/VBoxLinuxAdditions.run
#rm VBoxGuestAdditions_5.0.16.iso
#sudo umount /media/VBoxGuestAdditions
#sudo rmdir /media/VBoxGuestAdditions
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
   	    vb.memory = "2048"
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
   	   vb.memory = "4096"
       end
    db.vm.provision "shell", inline: $KerDev
  end
end
