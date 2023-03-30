# -*- mode: ruby -*-
# vi: set ft=ruby :


Vagrant.configure("2") do |config|

  if Vagrant.has_plugin?("vagrant-disksize") then
    config.disksize.size = '10GB'    
  end

  config.vm.box = "generic/debian9"
  config.vm.box_download_insecure=true

  config.vm.provider "virtualbox" do |vb|
    vb.gui = true

    vb.name = "debian9_vb"
    vb.cpus = "2"
    vb.memory = "2048"
  end

  provisioner = Vagrant::Util::Platform.windows? ? :guest_ansible : :ansible

  # Set utils, apache2 (port=8888), nginx (port=80), php5.6
  config.vm.provision provisioner do |ansible|
     ansible.playbook = "playbook_task4.yaml"
  end
  
  # Load index.php
  config.vm.provision provisioner do |ansible|
     ansible.playbook = "playbook_task5.yaml"
  end
  
  # Update php5.6 to php7.2
  config.vm.provision provisioner do |ansible|
     ansible.playbook = "playbook_task6.yaml"
  end

  config.vm.network "forwarded_port", guest: 80, host: 80, id: "nginx"
  config.vm.network "forwarded_port", guest: 8888, host: 8888, id: "apache"
end
