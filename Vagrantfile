# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "centos/7"
  #Configure X!1
  config.ssh.forward_agent = true
  config.ssh.forward_x11 = true
  config.vm.hostname = "shiloh"


  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
     vb.memory = "4096"
  end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Define a Vagrant Push strategy for pushing to Atlas. Other push strategies
  # such as FTP and Heroku are also available. See the documentation at
  # https://docs.vagrantup.com/v2/push/atlas.html for more information.
  # config.push.define "atlas" do |push|
  #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
  # end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
   config.vm.provision "shell", inline: <<-SHELL1
   	echo " update Yum"
	sudo yum -y update
   SHELL1
   config.vm.provision "shell", inline: <<-SHELL1
	echo "hello Lord Bryson welcome to a CENTOS env"
	sudo yum -y install git
        git config --global user.email "sidney@brysonworld.com"
        git config --global user.name "Dr. Sidney L. Bryson"
        git config --global push.default simple

	sudo yum -y install wget

   SHELL1

   config.vm.provision "shell", inline: <<-SHELL
	echo " Install podman "
	#cd /etc/yum.repos.d/
	#sudo wget https://download.opensuse.org/repositories/devel:kubic:libcontainers:stable/CentOS_7/devel:kubic:libcontainers:stable.repo
	sudo yum -y install podman
	sudo yum -y install buildah
	echo " ++++++++++++++++++++++++++++++++++++++++++++++"
	echo " Finished Podman  && Buidah Install "
   SHELL
  ## Let's pull in a shell script for provisioning
  #	 Bryson (c) 2020
  # sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'
   config.vm.provision "shell", inline: <<-SHELL
	echo  "++++++++++++++++++++++++++++++++++++++"
	echo  "                                       "
	echo  " Install VS Code 		"
	echo  "                                       "
	sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
	sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'

	sudo yum -y install code
   
   SHELL
   config.vm.provision "shell", inline: <<-SHELL
	echo " Install Node Js   "
	curl -sL https://rpm.nodesource.com/setup_10.x | sudo bash -
	sudo yum -y install nodejs
   SHELL
   #  Install the Google cloud sdk
   config.vm.provision "shell", inline: <<-SHELL
   sudo tee -a /etc/yum.repos.d/google-cloud-sdk.repo << EOM
[google-cloud-sdk]
name=Google Cloud SDK
baseurl=https://packages.cloud.google.com/yum/repos/cloud-sdk-el7-x86_64
enabled=1
gpgcheck=1
repo_gpgcheck=1
gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg
	https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
EOM
   SHELL
   config.vm.provision "shell", inline: <<-SHELL
	echo " Clone uservice directory "
	sudo git clone https://github.com/slbryson/uservice.git
        cd uservice
        sudo chown -R vagrant:vagrant * .
	npm install
	npm install express --save
   SHELL
   config.vm.provision "shell", inline: <<-SHELL
	sudo yum -y install google-cloud-sdk
	export PROJECT_ID=brysonmesh
   SHELL
#	cp /vagrant/brysonmesh-d44929299181.json $HOME/
#	cat brysonmesh-d44929299181.json |sudo podman login -u _json_key  --password-stdin https://gcr.io
   config.vm.provision "shell", inline: <<-SHELL
        sudo yum -y install centos-release-scl
        sudo yum -y install rh-python36
        scl enable rh-python36 bash

   SHELL
end
