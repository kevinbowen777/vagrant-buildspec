# -*- mode: ruby -*-
# vi: set ft=ruby :
require 'yaml'

BUILDSPEC = YAML.load_file('build_specs.yml')

Vagrant.configure('2') do |config|
  config.vm.box = BUILDSPEC['vagrant_box_name']
  #config.disksize.size = BUILDSPEC['disksize']
  config.ssh.insert_key = false

  config.vm.provider BUILDSPEC['provider'] do |v|
    v.cpus = BUILDSPEC['cpus']
    v.memory = BUILDSPEC['memory']
    v.customize ['modifyvm', :id, '--name',   BUILDSPEC['vbox_name']]
  end

  # Define host and networking
  config.vm.define BUILDSPEC['ansible_host'] do |host|
    config.vm.hostname = BUILDSPEC['hostname']
    config.vm.network :private_network, ip: BUILDSPEC['private_ip']
    #config.vm.network :public_network, ip: BUILDSPEC['public_ip']
  end

  BUILDSPEC['forwarded_port'].each do |port|
    config.vm.network :forwarded_port, guest: port['guest_port'], host: port['host_port']
  end

  BUILDSPEC['shared_dirs'].each do |dir|
    config.vm.synced_folder dir['guest_dir'], dir['host_dir'], disabled: false
  end

  # Ansible provisioning.
  config.vm.provision "ansible" do |ansible|
    ansible.compatibility_mode = "2.0"
    ansible.playbook = BUILDSPEC['playbook_location']
    ansible.inventory_path = BUILDSPEC['inventory']
  #  ansible.limit = 'all'
  end
end
