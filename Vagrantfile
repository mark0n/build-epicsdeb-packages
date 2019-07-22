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
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "debian/buster64"

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
  # config.vm.synced_folder "../data", "/vagrant_data"

  config.ssh.forward_agent = true

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
    vb.memory = "2048"
    vb.cpus = "4"
    vb.customize ["modifyvm", :id, "--ioapic", "on"]
  end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update -y > /dev/null
    apt-get install -y git-buildpackage > /dev/null

    gbp clone --debian-branch=uc3 https://github.com/mark0n/epics-debhelper.git
    cd epics-debhelper/
    gbp buildpackage -uc -us --git-debian-branch=uc3
    apt-get install -y dh-exec libparse-debcontrol-perl libtie-ixhash-perl > /dev/null
    dpkg -i /home/vagrant/{dh-exec-epics_8.19_all.deb,epics-debhelper_8.19_all.deb}
    cd /home/vagrant/

    gbp clone --debian-branch=debian10 https://github.com/mark0n/epics-base-package.git
    cd epics-base-package/
    apt-get install -y libreadline6-dev libncurses5-dev g++-mingw-w64 dh-systemd > /dev/null
    gbp buildpackage -uc -us --git-debian-branch=debian10
    cd /home/vagrant/
    dpkg -i *.deb

    gbp clone --debian-branch=v4.35 https://github.com/mark0n/asyn-1.git
    cd asyn-1/
    apt-get install -y libusb-1.0-0-dev
    gbp buildpackage -uc -us --git-debian-branch=v4.35
    cd /home/vagrant/
    dpkg -i *.deb

    gbp clone --debian-branch=v5.9 https://github.com/mark0n/autosave-package.git
    cd autosave-package/
    gbp buildpackage -uc -us --git-debian-branch=v5.9
    cd /home/vagrant/

    gbp clone --debian-branch=v3.6 https://github.com/mark0n/caputlog.git
    cd caputlog/
    apt-get install -y python3-sphinx
    gbp buildpackage -uc -us --git-debian-branch=v3.6
    cd /home/vagrant/

    gbp clone --debian-branch=v3.1.16 https://github.com/mark0n/deviocstats.git
    cd deviocstats/
    gbp buildpackage -uc -us --git-debian-branch=v3.1.16
    cd /home/vagrant/

    gbp clone --debian-branch=debian10 https://github.com/mark0n/seq.git
    cd seq/
    apt-get install -y re2c
    gbp buildpackage -uc -us --git-debian-branch=debian10
    cd /home/vagrant/
    dpkg -i epics-seq-dev_2.2.6-2_amd64.deb libseq2.2.6_2.2.6-2_amd64.deb

    gbp clone --debian-branch=v2.11.3 https://github.com/mark0n/sscan.git
    cd sscan/
    gbp buildpackage -uc -us --git-debian-branch=v2.11.3
    cd /home/vagrant/
    dpkg -i epics-sscan-dev_2.11.3-1_amd64.deb libepics-sscan2.11.3_2.11.3-1_amd64.deb

    gbp clone --debian-branch=v3.7.3 https://github.com/mark0n/calc.git
    cd calc/
    gbp buildpackage -uc -us --git-debian-branch=v3.7.3
    cd /home/vagrant/
    dpkg -i epics-calc-dev_3.7.3-1_amd64.deb libcalc3.7.3_3.7.3-1_amd64.deb

    gbp clone --debian-branch=v2.8.9 https://github.com/mark0n/stream.git
    cd stream/
    apt-get install -y libpcre3-dev
    gbp buildpackage -uc -us --git-debian-branch=v2.8.9
    cd /home/vagrant/

    gbp clone --debian-branch=v1.7.2 https://github.com/mark0n/busy.git
    cd busy/
    gbp buildpackage -uc -us --git-debian-branch=v1.7.2
    cd /home/vagrant/

    gbp clone --debian-branch=debian10 https://github.com/epicsdeb/cmake4epics.git
    cd cmake4epics/
    apt-get install -y cmake
    gbp buildpackage -uc -us --git-debian-branch=debian10
    cd /home/vagrant/

    gbp clone --debian-branch=debian10 https://github.com/mark0n/devlib2.git
    cd devlib2/
    gbp buildpackage -uc -us --git-debian-branch=debian10
    cd /home/vagrant/
    dpkg -i epics-devlib2-dev_2.10-2_amd64.deb libdevlib2.10_2.10-2_amd64.deb

    gbp clone --debian-branch=debian10 https://github.com/mark0n/mrfioc2-package.git
    cd mrfioc2-package/
    apt-get install -y dkms
    gbp buildpackage -uc -us --git-debian-branch=debian10
    cd /home/vagrant/

    gbp clone --debian-branch=v1.0.0.1 https://github.com/epicsdeb/epics-snmp.git
    cd epics-snmp/
    apt-get install -y libsnmp-dev
    gbp buildpackage -uc -us --git-debian-branch=v1.0.0.1
    cd /home/vagrant/

    gbp clone --debian-branch=debian10 https://github.com/epicsdeb/epics-mcore-utils.git
    cd epics-mcore-utils/
    gbp buildpackage -uc -us --git-debian-branch=debian10
    cd /home/vagrant/
  SHELL
end
