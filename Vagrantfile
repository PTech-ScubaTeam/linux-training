# -*- mode: ruby -*-
# vi: set ft=ruby

Vagrant.configure(2) do |config|
    config.vm.box = "ubuntu/trusty64"

    config.vm.provider "virtualbox" do |vb|
        vb.memory = "1024"
        vb.cpus = 1
    end

    config.vm.provision "shell", inline: <<-SHELL
        sudo apt-get update
        sudo apt-get install -y git python-pip python-dev build-essential zip
        sudo apt-get install -y dig whois
        sudo apt-get -y autoremove

        cd /vagrant
        sudo pip install -r requirements.txt

    SHELL

end
