# -*- mode: ruby -*-
# vi: set ft=ruby :

user = ENV['USER']

Vagrant.configure("2") do |config|
  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "generic/ubuntu2004"

  config.vm.define "#{user}-iac" do |machine1|
    # Disable automatic box update checking. If you disable this, then
    # boxes will only be checked for updates when the user runs
    # `vagrant box outdated`. This is not recommended.

    # Create a forwarded port mapping which allows access to a specific port
    # within the machine from a port on the host machine. In the example below,
    # accessing "localhost:8080" will access port 80 on the guest machine.
    # NOTE: This will enable public access to the opened port
#    machine1.vm.network "forwarded_port", guest: 80, host: 8080, id: "http"

    config.vm.network :private_network, ip: "192.168.121.120"

    # Create a private network, which allows host-only access to the machine
    # using a specific IP.
    # Share an additional folder to the guest VM. The first argument is
    # the path on the host to the actual folder. The second argument is
    # the path on the guest to mount the folder. And the optional third
    # argument is a set of non-required options.
    machine1.vm.synced_folder "../data", "/vagrant_data", create: true, group: "vagrant", owner: "vagrant"
    # Provider-specific configuration so you can fine-tune various
    # backing providers for Vagrant. These expose provider-specific options.
    # Example for VirtualBox:
    #
    machine1.vm.provider "libvirt" do |libvirt|
      libvirt.cpus = 1
      libvirt.memory = "2048"
    end
  end

  config.vm.provision :root_user, type: "shell", inline: "apt install python3"

  # Provisioning by Ansible playbooks
  config.vm.provision "ansible" do |ansible|
      ansible.compatibility_mode = "2.0"
      ansible.verbose = "vvv"
      ansible.playbook = "playbook/install.yml"
      ansible.become = true
  end
end
