# -*- mode: ruby -*-
# vi: set ft=ruby :

# README
#
# Getting Started:
# 1. vagrant plugin install vagrant-hostmanager
# 2. vagrant up
# 3. vagrant ssh
#
# This should put you at the control host
#  with access, by name, to other vms
#
Vagrant.configure(2) do |config|
  config.hostmanager.enabled = true

  config.vm.box = "generic/ubuntu1804"

  config.vm.define "control", primary: true do |h|
    h.vm.network "private_network", ip: "192.168.0.104"
    h.vm.provision :shell, :inline => <<'EOF'
if [ ! -f "/home/vagrant/.ssh/id_rsa" ]; then
  ssh-keygen -t rsa -N "" -f /home/vagrant/.ssh/id_rsa
fi

cat << 'SSHEOF' > /home/vagrant/.ssh/config
Host *
  StrictHostKeyChecking no
  UserKnownHostsFile=/dev/null
SSHEOF

chown -R vagrant:vagrant /home/vagrant/.ssh/
EOF
  end

  config.vm.define "lb01" do |h|
    h.vm.network "private_network", ip: "192.168.0.101"
  end

  config.vm.define "app01" do |h|
    h.vm.network "private_network", ip: "192.168.0.102"
  end

  config.vm.define "app02" do |h|
    h.vm.network "private_network", ip: "192.168.0.103"
  end
end
