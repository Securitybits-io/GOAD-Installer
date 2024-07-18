# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/jammy64"

  config.vm.hostname = "GOAD-Installer"

  config.vm.provider "virtualbox" do |v|
    v.memory = 1000
    v.cpus = 1
    v.name = "GOAD-Installer"
    v.customize ["modifyvm", :id, "--groups", "/GOAD Management"]
  end

  config.vm.network :private_network, ip: "192.168.56.10"

  $dependencies = <<-DEPS
  sudo apt update
  sudo apt install -y git python3-pip sshpass lftp rsync openssh-client
  DEPS
  
  $pip = <<-PIP
  python3 -m pip install --upgrade pip
  python3 -m pip install --upgrade ansible-core==2.12.6
  python3 -m pip install --upgrade pywinrm
  PIP

  $goat = <<-GOAT
  git clone https://github.com/Orange-Cyberdefense/GOAD
  cd GOAD/ansible
  ansible-galaxy install -r requirements.yml
  GOAT
  
  config.vm.provision "shell", inline: $dependencies
  config.vm.provision "shell", inline: $pip
  config.vm.provision "shell", inline: $goat
end
