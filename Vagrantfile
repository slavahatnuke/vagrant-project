require 'json'

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  settings = JSON.parse(IO.read('Vagrantfile.settings.json'))

  ## Box
  config.vm.box = settings["box"]
  config.vm.box_url = settings["box_url"]

  config.vm.guest = settings["guest"]

  ## Network
  config.vm.network :private_network, ip: settings['ip']

  ## Network/Ports
  settings["ports"].each do |key, value|
    config.vm.network :forwarded_port, guest: Integer(key), host: Integer(value)
  end

  ## Sync
  settings["sync"].each do |key, value|
    config.vm.synced_folder key, value, :nfs => settings["nfs"]
  end

  ## Provision
  config.vm.provision "shell", inline: settings['provision']

  ## Properties
  config.vm.provider :virtualbox do |vb|

    vb.gui = settings['gui']
    vb.name = settings['project']

    vb.customize ["modifyvm", :id, "--memory", settings['memory']]
    vb.customize ["modifyvm", :id, "--cpus", settings['cpus']]

    vb.customize ["modifyvm", :id, "--acpi", settings['acpi']]
    vb.customize ["modifyvm", :id, "--ioapic", settings['ioapic']]
    vb.customize ["modifyvm", :id, "--vram", settings['vram']]

    # vb.customize ["storageattach", :id, "--storagectl", "SATA Controller", '--port', '0', '--nonrotational', 'on']
  end

end