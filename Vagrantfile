# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.define "dockertest" do |dockertest|
  dockertest.vm.box = "centos/7"
  dockertest.vm.hostname = "dockertest"
  dockertest.vm.network "private_network", ip: "192.168.33.10"
  dockertest.vm.network "forwarded_port", guest: 80, host: 8080
 #dockertest.vm.network "forwarded_port", guest: 9093, host: 9093
 #dockertest.vm.network "forwarded_port", guest: 2181, host: 2181
 #dockertest.vm.network "forwarded_port", guest: 9092, host: 9092	 
  dockertest.vm.provider "virtualbox" do |vb|
  vb.memory = "4048"
  end
  dockertest.vm.synced_folder ".", "/vagrant", disabled: true
  dockertest.vm.provision "shell", inline: <<-SHELL
  yum update
  yum install epel-release -y
  yum install -y ansible pyOpenSSL python-cryptography python-lxml
  yum install java-1.8.0-openjdk-headless -y
  yum install httpd-tools
  yum install git* -y
  SHELL
  end
  end