# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrant configuration using version 2.
Vagrant.configure("2") do |config|
  # Define the base box.
  config.vm.box = "ubuntu/bionic64"
  config.vm.boot_timeout = 600

  # Network configurations.
  config.vm.network "public_network", type: "dhcp"
  config.vm.network "private_network", ip: "192.168.1.10"

  # Hostname.
  config.vm.hostname = "server"

  # VirtualBox provider-specific settings.
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "4096"  # RAM in MB
    vb.cpus = 8          # Number of CPUs
  end

  # Synced folder.
  config.vm.synced_folder "./CONFIG", "/vagrant_config/CONFIG"

  # Provisioning with shell script.
  config.vm.provision "shell", inline: <<-SHELL

    sudo su
    
    echo "DHCP Server"
    apt-get update && apt-get upgrade
    apt-get install -y net-tools
    apt-get install -y isc-dhcp-server

    echo "Configuring DHCP Server"
    mv /etc/default/isc-dhcp-server /etc/default/isc-dhcp-server.bkp
    cp /vagrant_config/CONFIG/DHCPD/isc-dhcp-server /etc/default/isc-dhcp-server
    mv /etc/dhcp/dhcpd.conf /etc/dhcp/dhcpd.conf.bkp
    cp /vagrant_config/CONFIG/DHCPD/dhcpd.conf /etc/dhcp/dhcpd.conf

    systemctl restart isc-dhcp-server
    systemctl status isc-dhcp-server

    echo "DNS Server"
    apt-get install -y bind9
    
    mv /etc/bind/named.conf.options /etc/bind/named.conf.options.bkp
    cp /vagrant_config/CONFIG/DNS/named.conf.options /etc/bind/named.conf.options
    mv /etc/bind/named.conf.local /etc/bind/named.conf.local.bkp
    cp /vagrant_config/CONFIG/DNS/named.conf.local /etc/bind/named.conf.local
    mv /etc/bind/db.local /etc/bind/db.local.bkp
    cp /vagrant_config/CONFIG/DNS/db.local /etc/bind/db.local

    systemctl restart bind9
    systemctl status bind9

    echo "APACHE2 Web"
    apt-get install -y apache2

    cp /vagrant_config/CONFIG/APACHE2/www.teste.local.conf /etc/apache2/sites-available/www.teste.local.conf

    sudo a2ensite www.teste.local.conf
    sudo systemctl reload apache2

    echo "FTP Server"
    apt-get install -y proftpd

    mkdir -p ~/share
   
    mv /etc/proftpd/proftpd.conf /etc/proftpd/proftpd.conf.bkp
    cp /vagrant_config/CONFIG/FTP/proftpd.conf /etc/proftpd/proftpd.conf

    service proftpd restart

    if ! id "webmaster" &>/dev/null; then
      useradd webmaster -d /root/share -s /bin/false
      echo "Usuário webmaster criado"
    else
      echo "Usuário webmaster já existe"
    fi

  chown webmaster -R ~/share

  SHELL
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

  # Disable the default share of the current code directory. Doing this
  # provides improved isolation between the vagrant box and your host
  # by making sure your Vagrantfile isn't accessible to the vagrant box.
  # If you use this you may want to enable additional shared subfolders as
  # shown above.
  # config.vm.synced_folder ".", "/vagrant", disabled: true

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
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELLa
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
