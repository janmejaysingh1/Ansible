# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.define "dockertest" do |dockertest|
  dockertest.vm.box = "centos/7"
  dockertest.vm.box_version = "1811.02"
  dockertest.vm.hostname = "dockertest"
  dockertest.vm.network "private_network", ip: "192.168.33.10"
  dockertest.vm.network "forwarded_port", guest: 80, host: 8080
  dockertest.vm.network "forwarded_port", guest: 443, host: 443
 #dockertest.vm.network "forwarded_port", guest: 2181, host: 2181
 #dockertest.vm.network "forwarded_port", guest: 9092, host: 9092	 
  dockertest.vm.provider "virtualbox" do |vb|
  vb.memory = "4048"
  vb.cpus = "2"
  end
  dockertest.vm.synced_folder ".", "/home/vagrant",  :mount_options => ["dmode=777", "fmode=666"]
  dockertest.vm.provision "shell", inline: <<-SHELL
  sudo sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config; sudo systemctl restart sshd;, run: "always"
  echo "Installing updates"
  yum update -y
  echo "Installing epel-release"
  yum instal wget -y
  wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
  echo "Installing epel-release1"
  yum install epel-release -y
  echo "Installing ansible"
  yum install -y ansible pyOpenSSL python-cryptography python-lxml
  echo "Installing openjdk-headless"
  yum install java-1.8.0-openjdk-headless -y
  echo "Installing httpd"
  yum install httpd-tools
  echo "Installing git"
  yum install git -y
  echo "Installing openshif file"
  mkdir -p /home/vagrant
  echo "Installing openshif file move"
  cd /home/vagrant
  echo "Installing openshift git clone"
  git clone -b release-3.11 https://github.com/openshift/openshift-ansible.git --depth 1
  echo "Installing openshif file"
  cd openshift-ansible
  echo "Installing runing play book 1"
  sudo ansible-playbook -i inventory/hosts.localhost playbooks/prerequisites.yml >/home/vagrant/prerequisites.log &
  echo "Installing runing play book 1"
  sudo ansible-playbook -i inventory/hosts.localhost playbooks/deploy_cluster.yml >/home/vagrant/deploy_cluster.log &
  SHELL
  end
  end