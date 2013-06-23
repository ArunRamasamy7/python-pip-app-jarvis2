# -*- mode: ruby -*-
# vi: set ft=ruby :

$script = <<SCRIPT
  # Ensure noninteractive apt-get
  export DEBIAN_FRONTEND=noninteractive

  # Use Norwegian mirror
  sed -i -e 's/us\.archive\.ubuntu\.com/no.archive.ubuntu.com/' \
          /etc/apt/sources.list
  apt-get -y update

  # Set time zone
  echo "Europe/Oslo" > /etc/timezone
  dpkg-reconfigure tzdata

  # Install packages
  apt-get -y install python-pip python-dev libxml2-dev libxslt1-dev

  # Install pip packages
  pip install --use-mirrors -r /vagrant/requirements.txt
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"
  config.ssh.forward_agent = true
  config.vm.provision :shell, :inline => $script
  config.vm.network :forwarded_port, guest: 5000, host: 5000
end