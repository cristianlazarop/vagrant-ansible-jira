# -*- mode: ruby -*-
# vi: set ft=ruby :
BOX_IMAGE = "gunnix/ubuntu_server_20.04.1_LTS"
# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  config.vm.define "postgres" do |postgres|
    postgres.vm.box = BOX_IMAGE
    postgres.vm.box_version = "0.0.1"
    postgres.vm.hostname = "postgres"
    postgres.vm.network :private_network, ip: "192.168.33.13"
    postgres.vm.network "forwarded_port", guest: 5432, host: 5432
    postgres.vm.provision "shell", inline: "apt-get update && apt-get -y install git wget curl vim net-tools jq ncdu axel open-vm-tools tcptraceroute python3-pip python3-setuptools"
  
    postgres.vm.provision "ansible" do |ansible|
        ansible.playbook = "./01_postgres_config/playbook.yml"
  
      end
end
  config.vm.define "jira" do |jira|

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  jira.vm.box = BOX_IMAGE
  jira.vm.box_version = "0.0.1"
    # config.vm.box = "jira-liza-imported.box"
    jira.vm.network "private_network", ip: "192.168.33.10"
    jira.vm.synced_folder "data/", "/home/vagrant/vagrant_data"

    jira.vm.provision :ansible do |ansible|
    ansible.playbook = "play.yml"
  end
end



  config.vm.provider "virtualbox" do |v|
    v.memory = 2048
    v.cpus = 4
  end

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"
  # config.vm.network "forwarded_port", guest: 8080, host: 8888

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL

end
