require 'json'

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  settings = JSON.parse(IO.read('Vagrantfile.settings.json'))

  ## Box
  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"

  config.vm.guest = :ubuntu

  ## Network
  config.vm.network :private_network, ip: settings['private_ip']

  ## Network/Ports
  # config.vm.network :forwarded_port, guest: 80, host: 8080
  # config.vm.network :forwarded_port, guest: 3306, host: 3307

  ## Sync
  config.vm.synced_folder "project", "/project", :nfs => true
  config.vm.synced_folder "provision", "/provision", :nfs => true

  ## Provision

  # Initial / Install
  config.vm.provision "shell", inline: settings['provision']

  ## Properties
  config.vm.provider :virtualbox do |vb|

    vb.gui = settings['gui']
    vb.name = settings['project']

    vb.customize ["modifyvm", :id, "--memory", settings['memory']]
    vb.customize ["modifyvm", :id, "--cpus", settings['cpus']]

    vb.customize ["modifyvm", :id, "--acpi", "on"]
    vb.customize ["modifyvm", :id, "--ioapic", "on"]
    vb.customize ["modifyvm", :id, "--vram", settings['vram']]

    vb.customize ["storageattach", :id, "--storagectl", "SATA Controller", '--port', '0', '--nonrotational', 'on']
  end

end