# -*- mode: ruby -*-
# vi: set ft=ruby :
$hostsfile_update = <<-'SCRIPT'
echo -e '192.168.50.110 control.example.com control\n192.168.50.111 node1.example.com node1\n192.168.50.112 node2.example.com node2' >> /etc/hosts
sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config && systemctl restart sshd
SCRIPT

Vagrant.configure("2") do |config|

  config.vm.define "control", primary: true do |control|
    control.vm.box = "centos/7"
    control.vm.hostname = "control.example.com"
    control.vm.network "private_network", ip: "192.168.50.110"
    control.vm.provision "shell", inline: $hostsfile_update
  end

  config.vm.define "node1" do |node1|
    node1.vm.box = "centos/7"
    node1.vm.hostname = "node1.example.com"
    node1.vm.network "private_network", ip: "192.168.50.111"
    node1.vm.provision "shell", inline: $hostsfile_update
  end

  config.vm.define "node2" do |node2|
    node2.vm.box = "centos/7"
    node2.vm.hostname = "node2.example.com"
    node2.vm.network "private_network", ip: "192.168.50.112"
    node2.vm.provision "shell", inline: $hostsfile_update
  end

end
