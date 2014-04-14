# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

ENV['VAGRANT_DEFAULT_PROVIDER'] = 'lxc'

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.define "rabbitmq" do |rabbitmq|
    rabbitmq.vm.provider :lxc do |lxc|
      # Same effect as as 'customize ["modifyvm", :id, "--memory", "1024"]' for VirtualBox
      lxc.customize 'cgroup.memory.limit_in_bytes', '512M'
      lxc.customize 'network.ipv4',                 '10.0.3.10/24'
      lxc.customize 'aa_profile',                   'unconfined'
    end

    # Every Vagrant virtual environment requires a box to build off of.
    rabbitmq.vm.box = "precise64-lxc"

    # The url from where the 'rabbitmq.vm.box' box will be fetched if it
    # doesn't already exist on the user's system.
    rabbitmq.vm.box_url = "https://dl.dropboxusercontent.com/s/wy1k8zam887sxlv/vagrant-lxc-precise-amd64-2014-01-07.box?token_hash=AAEc5VxoqUxuX5koDFv_fpc4bcwkx0V7OjRj-EusjhMSkA"

    # Share an additional folder to the guest VM. The first argument is
    # the path on the host to the actual folder. The second argument is
    # the path on the guest to mount the folder. And the optional third
    # argument is a set of non-required options.
    # rabbitmq.vm.synced_folder "../data", "/vagrant_data"
    rabbitmq.vm.synced_folder "/lib/modules", "/lib/modules"

    rabbitmq.vm.provision "ansible" do |ansible|
      ansible.limit = 'all'
      ansible.inventory_path    = "development"
      ansible.playbook          = "rabbitmqservers.yml"
      ansible.sudo              = true
      ansible.host_key_checking = false
    end
  end
end
