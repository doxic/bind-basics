# -*- mode: ruby -*-
# vi: set ft=ruby :

#$shell_script = <<SCRIPT
#SCRIPT

Vagrant.configure("2") do |config|

  config.vm.define "nixsrv001" do |machine|
    machine.vm.box = "centos/7"
    machine.vm.hostname = 'nixsrv001'

    machine.vm.network :private_network, ip: "192.168.56.100",
      virtualbox__intnet: "DHCPScope"
    #machine.vm.network :forwarded_port, guest: 22, host: 1022, id: "ssh"

    machine.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--name", "nixsrv001"]
      v.customize ["modifyvm", :id, "--clipboard", "bidirectional"]
      v.linked_clone = true if Vagrant::VERSION =~ /^1.8/
    end
  end

    config.vm.define "nixsrv002" do |machine|
      machine.vm.box = "centos/7"
      machine.vm.hostname = 'nixsrv002'

      machine.vm.network :private_network, ip: "192.168.56.101",
        virtualbox__intnet: "DHCPScope"
      #machine.vm.network :forwarded_port, guest: 22, host: 2022, id: "ssh"

      machine.vm.provider :virtualbox do |v|
        v.customize ["modifyvm", :id, "--name", "nixsrv002"]
        v.customize ["modifyvm", :id, "--clipboard", "bidirectional"]
        v.linked_clone = true if Vagrant::VERSION =~ /^1.8/
      end
  end

  config.vm.define "ctrsrv001" do |machine|
    machine.vm.box = "centos/7"
    machine.vm.hostname = 'ctrsrv001'

    machine.vm.network :private_network, ip: "192.168.56.50",
      virtualbox__intnet: "DHCPScope"
    #machine.vm.network :forwarded_port, guest: 22, host: 3022, id: "ssh"

    machine.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--name", "ctrsrv001"]
      v.customize ["modifyvm", :id, "--clipboard", "bidirectional"]
      v.linked_clone = true if Vagrant::VERSION =~ /^1.8/
    end

    machine.vm.provision :ansible_local do |ansible|
      ansible.playbook       = "provisioning/playbook.yml"
      ansible.verbose        = true
      ansible.install        = true
      ansible.limit          = "all" # or only "nodes" group, etc.
      ansible.inventory_path = "provisioning/staging"
    end
    #machine.vm.provision "shell", path: "scripts/bootstrap-machine.sh"

  end
end
