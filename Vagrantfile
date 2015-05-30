# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = "ubuntu/trusty64"
  config.vm.network :private_network, ip: "10.1.0.2", :netmask => "255.255.0.0"

  config.vm.provider :virtualbox do |v|
    v.memory = 1024
    v.customize ["modifyvm", :id, "--nicpromisc2", "allow-vms"]
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "getreqs.yml"
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "prepare-vm.yml"
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "deploy.yml"
    ansible.extra_vars = {
      openstack_network_external_device: "eth1",
      openstack_network_external_gateway: "10.1.0.2"
    }
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "test.yml"
  end

end
