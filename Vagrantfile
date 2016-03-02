# -*- mode: ruby -*-
# vi: set ft=ruby :

def create_synced_dir(config, host_dir, vm_dir, options = {})
  config.vm.synced_folder host_dir, vm_dir, options if File.directory?(host_dir)
end

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  if Vagrant.has_plugin?("vagrant-cachier")
    # Configure cached packages to be shared between instances of the same base box.
    # More info on http://fgrehm.viewdocs.io/vagrant-cachier/usage
    config.cache.scope = :box
  end

  config.vm.box = "workshop"
  config.vm.hostname = "blog"
  config.ssh.username = 'vagrant'
  config.ssh.password = 'vagrant'
  config.ssh.insert_key = true

  config.vm.define "blog" do |t|
  end

  #create_synced_dir(config, "../../cache/m2/", "/home/vagrant/.m2", { create: true })

  # Ghost Blog
  config.vm.network "forwarded_port", guest: 2368, host: 2368

  config.vm.network "private_network", ip: "192.168.33.10"
  config.vm.hostname = "tiago.griffo.me"

  config.vm.provider "virtualbox" do |vb|
     # Recommended specs for VM
     vb.customize ["modifyvm", :id, "--memory", "3584"]
     vb.customize ["modifyvm", :id, "--cpus", "2"]

     # Minimum specs for VM - For any wosk station with < 4GB RAM and < 2CPU
     # vb.customize ["modifyvm", :id, "--memory", "2048"]
     # vb.customize ["modifyvm", :id, "--cpus", "1"]
  end
end
