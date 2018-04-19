# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.define "drone"
  config.vm.box = "centos/7"

  config.vm.network "forwarded_port", guest: 80, host: 8000

  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.vm.provider "virtualbox" do |vitualbox|
  end

  config.vm.provider :digital_ocean do |provider, override|
    override.ssh.private_key_path = '~/.ssh/id_rsa'
    override.vm.box = 'digital_ocean'
    override.vm.box_url = "https://github.com/devopsgroup-io/vagrant-digitalocean/raw/master/box/digital_ocean.box"

    provider.token = ENV['DIGITALOCEAN_TOKEN']
    provider.ssh_key_name = ENV['DIGITALOCEAN_KEY_NAME']
    provider.image = 'centos-7-x64'
    provider.region = 'ams3'
    provider.size = 's-1vcpu-1gb'
  end

  config.vm.provision "ansible" do |ansible|
    ansible.galaxy_role_file = 'ansible/requirements.yml'
    ansible.playbook = "ansible/playbook.yml"
    ansible.become = true
  end
	
end
