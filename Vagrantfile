# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/jammy64"

  config.vm.hostname = "GOAD-Installer"

  config.vm.provider "virtualbox" do |v|
    v.memory = 2000
    v.cpus = 1
    v.name = "GOAD-Installer"
    v.customize ["modifyvm", :id, "--groups", "/GOAD Management"]
  end

  config.vm.network :private_network, type: "dhcp"

  $script = <<-SCRIPT
  sudo apt install -y git sshpass lftp rsync openssh-client
  git clone git@github.com:Orange-Cyberdefense/GOAD.git
  sudo apt install python3-pip
  python3 -m pip install --upgrade pip
  python3 -m pip install --upgrade ansible-core==2.12.6
  python3 -m pip install --upgrade pywinrm
  SCRIPT
  
  Vagrant.configure("2") do |config|
    config.vm.provision "shell", inline: $script
  end

end
