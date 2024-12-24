# -*- mode: ruby -*-
# vi: set ft=ruby :
#
Vagrant.configure("2") do |config|
  config.vm.box = "debian/bookworm64"
  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.vm.define "bastiao" do |node|
    node.vm.hostname = "bastiao.internal"
    node.vm.network "private_network", ip: "10.1.0.10"

    node.vm.provider :virtualbox do |domain|
      domain.memory = 1096
      domain.cpus = 1
    end
  end

  (1..1).each do |j|
    config.vm.define "lb#{j}" do |node|
      node.vm.hostname = "lb#{j}.internal"
      node.vm.network "private_network", ip: "10.1.0.9#{j}"
      node.vm.network "public_network",
          use_dhcp_assigned_default_route: true
      node.vm.provider :virtualbox do |domain|
        domain.memory = 512
        domain.cpus = 1
      end
    end
  end

  config.vm.define "kmaster1" do |node|
    node.vm.hostname = "kmaster1.internal"
    node.vm.network "private_network", ip: "10.1.0.11"
  # Configuração da interface de rede
    node.vm.network "public_network", bridge: "wlo1" # Interface pública ligada à sua Wi-Fi
    node.vm.provider :virtualbox do |domain|
      domain.memory = 8096
      domain.cpus = 4
    end
  end

  config.vm.define "cpk8s01" do |node| 
    node.vm.hostname = "cpk8s01.internal"
    node.vm.network "private_network", ip: "10.1.0.101"
  # Configuração da interface de rede
    node.vm.network "public_network", bridge: "wlo1" # Interface pública ligada à sua Wi-Fi
    node.vm.provider :virtualbox do |domain|
      domain.memory = 8096
      domain.cpus = 4
    end
  end
    # Define que nenhuma interface NAT será criada
 

  (1..1).each do |j|
    config.vm.define "knode#{j}" do |node|
      node.vm.hostname = "knode#{j}.internal"
      node.vm.network "private_network", ip: "10.1.0.2#{j}"

      node.vm.provider :virtualbox do |domain|
        domain.memory = 2048
        domain.cpus = 2
      end
    end
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"
    ansible.groups = {
      "kubernetes" => ["kmaster1", "cpk8s01", "knode1", "knode2"], 
      "master_root" => ["kmaster1", "cpk8s01"],
      "workers" => ["knode1", "knode2"],
    }
  end
end
