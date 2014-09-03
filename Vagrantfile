# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

$script = <<-SCRIPT
sed -i s/archive.ubuntu.com/ftp.jaist.ac.jp/ /etc/apt/sources.list
apt-get update
apt-get install -y openjdk-7-jre-headless unzip
su -l vagrant -c "
unzip -q /vagrant/biserver-ce-5.1.0.0-752.zip -d /home/vagrant
cd /home/vagrant/biserver-ce
./start-pentaho.sh
"
SCRIPT

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.host_name = "5min-pentaho-biserver"
  config.vm.box = "ubuntu/trusty32"
  config.vm.network :private_network, ip: "192.168.33.10"
  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "2048"]
  end

  config.vm.provision "shell", inline: $script
end
