# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  config.vm.box = "hashicorp/precise64"

  config.vm.network "forwarded_port", guest: 3000, host: 3000

  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y curl postgresql postgresql-server-dev-9.1 nodejs
    ln -s /vagrant /twitter-clone
  SHELL

  config.vm.provision "shell", privileged: false, inline: <<-SHELL
    gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
    \\curl -sSL https://get.rvm.io | bash -s stable
    source /home/vagrant/.rvm/scripts/rvm
    rvm install 2.2.2
    rvm --default use 2.2.2
    gem install rails -v '4.2.4' --no-document
    gem install pg --no-document

    # This only needed to be done on initial project setup
    # rails new /twitter-clone --database=postgresql --skip-turbolinks
  SHELL
end
