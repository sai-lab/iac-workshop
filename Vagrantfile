# -*- mode: ruby -*-
# vi: set ft=ruby :

user = ENV['USER']

Vagrant.configure("2") do |config|
  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "generic/ubuntu2004"

  config.vm.define "#{user}-iac" do |machine|
    # Disable automatic box update checking. If you disable this, then
    # boxes will only be checked for updates when the user runs
    # `vagrant box outdated`. This is not recommended.

    # Create a forwarded port mapping which allows access to a specific port
    # within the machine from a port on the host machine. In the example below,
    # accessing "localhost:8080" will access port 80 on the guest machine.
    # NOTE: This will enable public access to the opened port
    # machine1.vm.network "forwarded_port", guest: 80, host: 8080, id: "http"

    # Share an additional folder to the guest VM. The first argument is
    # the path on the host to the actual folder. The second argument is
    # the path on the guest to mount the folder. And the optional third
    # argument is a set of non-required options.
    machine.vm.synced_folder "../data", "/vagrant_data", create: true, group: "vagrant", owner: "vagrant"

    machine.vm.provider "libvirt" do |libvirt|
      libvirt.cpus = 1
      libvirt.memory = "2048"
    end
  end

  config.vm.provision :root_user, type: "shell", inline: "apt-get install python3"

  # Provisioning by Ansible playbooks
  config.vm.provision "ansible" do |ansible|
      ansible.compatibility_mode = "2.0"
      #ansible.verbose = "vvv"
      ansible.playbook = "playbook/install.yml"
      ansible.become = true
  end
end
