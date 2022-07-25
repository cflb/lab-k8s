# -*- mode: ruby -*-
# vi: set ft=ruby :
#

ENV['VAGRANT_DEFAULT_PROVIDER'] = 'libvirt'
Vagrant.configure("2") do |config|
  config.vm.box = "debian/buster64"
  config.vm.synced_folder ".", "/vagrant", disabled: false

  (1..1).each do |i|
    config.vm.define "masternode#{i}" do |node|
      node.vm.hostname = "masternode#{i}.l4b"
      node.vm.network "private_network", ip: "10.2.0.1#{i}"

      node.vm.provider :libvirt do |domain|
        domain.driver = "qemu"
        domain.memory = 2024
        domain.cpus = 2
      end
    end
  end

  (1..2).each do |j|
    config.vm.define "workernode#{j}" do |node|
      node.vm.hostname = "workernode#{j}.l4b"
      node.vm.network "private_network", ip: "10.2.0.2#{j}"

      node.vm.provider :libvirt do |domain|
        domain.driver = "qemu"
        domain.memory = 1024
        domain.cpus = 1
      end
    end
  end

  #(1..1).each do |k|
  #  config.vm.define "router#{k}" do |node|
  #    node.vm.hostname = "router#{k}.l4b"
  #    node.vm.network "private_network", ip: "10.2.0.4#{k}"
  #
  #    node.vm.provider :libvirt do |domain|
  #      domain.driver = "qemu"
  #      domain.memory = 768
  #      domain.cpus = 1
  #    end
  #  end
  #end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yaml"
    ansible.groups = {
      "kubernetes" => ["masternode1", "workernode1", "workerpnode2"],
      "master_root" => ["masternode1"],
      "masters" => ["masternode1", "masternode2"],
      "workers" => ["workernode1", "workernode2"],
      #"router_root" => ["router1"],
      #"routers" => ["router1"],
      #"storages" => [""]
    }
  end
end
