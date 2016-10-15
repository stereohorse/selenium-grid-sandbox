# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"

  config.vm.define "vm1" do |vm1|
    vm1.vm.network "private_network", ip: "192.168.5.2"
    vm1.vm.hostname = "overlord"

    vm1.vm.provider "virtualbox" do |v|
      v.memory = 512
      v.cpus = 1
    end
  end

  config.vm.define "vm2" do |vm2|
    vm2.vm.network "private_network", ip: "192.168.5.3"
    vm2.vm.hostname = "gremlin1"

    vm2.vm.provider "virtualbox" do |v|
      v.memory = 2048
      v.cpus = 2
    end
  end

  config.vm.define "vm3" do |vm3|
    vm3.vm.network "private_network", ip: "192.168.5.4"
    vm3.vm.hostname = "gremlin2"

    vm3.vm.provider "virtualbox" do |v|
      v.memory = 1024
      v.cpus = 1
    end
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "play-site.yml"
    ansible.groups = {
      "docker" => ["vm1", "vm2", "vm3"],
      "docker:vars" => {
        "ssh_user" => "vagrant"
      },

      "masters" => ["vm1"],
      "masters:vars" => {
        "consul_addr" => "192.168.5.2:8500"
      },

      "slaves" => ["vm2", "vm3"],
      "slaves:vars" => {
        "consul_addr" => "192.168.5.2:8500"
      },
    }
  end

end
