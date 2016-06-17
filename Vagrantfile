# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "geerlingguy/ubuntu1404"
  config.vm.network :private_network, ip: "192.168.88.8"
  config.ssh.insert_key = false

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "512"]
    vb.customize ["modifyvm", :id, "--cpus", "1"]
    vb.customize ["modifyvm", :id, "--cpuexecutioncap", "50"]
  end

  config.vm.provider :linode do |provider, override|
    override.ssh.private_key_path = '~/.ssh/id_rsa'
    override.vm.box = 'linode'
    override.vm.box_url = "https://github.com/displague/vagrant-linode/raw/master/box/linode.box"
    provider.api_key = 'AETqyuH0FfNTlQXP6sUnuU0W72XrN2ssC0N7ZtsB7cJQKFmp7hDnknRNYuMxlCU9'
    provider.distribution = 'Ubuntu 14.04 LTS'
    provider.datacenter = 'london'
    provider.plan = 'Linode 2048'
    provider.private_networking = true
  end

  # Ansible provisioning.
  config.vm.provision "ansible" do |ansible|
    ansible.inventory_path = "./provisioning/hosts/development"
    ansible.playbook = "provisioning/site.yml"
    ansible.sudo = true
    # ansible.verbose = "vvv"
  end
end
