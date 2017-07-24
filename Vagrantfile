## Creating multiple nodes using Vagrant

## Script to install necessary packages and ansible for Centos test box.
## Comment out anything you do not want to install
$update_ansible_centos = <<-SCRIPT
cat << EOF
--------- Installing Updates ---------
    ()
   () ____
 _||__|  |  ______   ______   ______
(        | |      | |      | |      |
/-()---() ~ ()--() ~ ()--() ~ ()--()
--------------------------------------
EOF
yum update
yum install epel-release -y
yum install git
yum install vim
yum install ansible -y
SCRIPT

## Script to install necessary packages and ansible for Ubuntu test box.
## Comment out anything you do not want to install
$update_ansible_ubuntu = <<-SCRIPT
cat << EOF
--------- Installing Updates ---------
    ()
   () ____
 _||__|  |  ______   ______   ______
(        | |      | |      | |      |
/-()---() ~ ()--() ~ ()--() ~ ()--()
--------------------------------------
EOF
apt-get -y install software-properties-common
apt-add-repository -y ppa:ansible/ansible
apt-get -y update
apt-get -y install ansible
SCRIPT

## Here you can define as many servers you want and their specifications.
## The box defines the OS, and it can be changed
servers=[
      {
        :hostname => "app",
        :ip => "192.168.100.10",
        :box => "bento/centos-7.3",
        :ram => 1024,
        :cpu => 1
      },
      {
        :hostname => "web",
        :ip => "192.168.100.11",
        :box => "bento/centos-7.3",
        :ram => 2048,
        :cpu => 2
      }
    ]

Vagrant.configure("2") do |config|
    servers.each do |machine|
        config.vm.define machine[:hostname] do |node|
            node.vm.box = machine[:box]
            node.vm.hostname = machine[:hostname]
            node.vm.network "private_network", ip: machine[:ip]
            node.ssh.insert_key = true
            node.vm.provider "virtualbox" do |vm|
                vm.customize ["modifyvm", :id, "--memory", machine[:ram]]
                vm.customize ["modifyvm", :id, "--cpus", machine[:cpu]]
            end
            node.vm.provision "shell", inline: $update_packages_centos ## change it to the ubuntu script if the OS is ubuntu
        end
    end
end
