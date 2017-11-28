# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.box = "bento/ubuntu-16.04"

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
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  config.vm.synced_folder "~/opt/vagrant_data", "/vagrant_data"

  config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
    # vb.gui = true

    # Customize the amount of memory on the VM:
    vb.memory = "2048"
  end

  config.vm.provision "shell", inline: <<-SHELL
    add-apt-repository universe
    add-apt-repository ppa:wireshark-dev/stable
    add-apt-repository ppa:neovim-ppa/stable

    apt-get update
    apt-get install -y can-utils xfce4 virtualbox-guest-dkms virtualbox-guest-utils virtualbox-guest-x11 xserver-xorg-legacy
    apt-get install -y wireshark wireshark-common

    apt-get install -y software-properties-common
    apt-get install -y neovim

    apt-get install -y python-pip python-dev build-essential
    pip install --upgrade pip
    pip install --upgrade virtualenv

    apt-get install -y python3-dev python3-pip python3-setuptools
    pip3 install --upgrade pip
    pip3 install --upgrade virtualenv
    pip3 install --upgrade neovim
    chown -R vagrant.vagrant .local

    sed -i 's/allowed_users=.*$/allowed_users=anybody/' /etc/X11/Xwrapper.config
    VBoxClient-all
  SHELL
end
