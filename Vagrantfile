server_ip     = "192.168.99.30"
hostname      = "development.nodejs.local"

Vagrant.configure("2") do |config|
  config.vm.box = "precise32"

  config.vm.box_url = "http://files.vagrantup.com/precise32.box"

  # config.vm.share_folder "app", "/home/vagrant/app", "app"
  config.vm.hostname = hostname

    config.vm.network :private_network, ip: server_ip
    config.ssh.forward_agent = true
    config.vm.network :forwarded_port, guest: 3000, host: 3000

    config.vm.synced_folder "~/Projects", "/vagrant", type: "nfs"


  # Uncomment the following line to allow for symlinks
  # in the app folder. This will not work on Windows, and will
  # not work with Vagrant providers other than VirtualBox
  # config.vm.customize ["setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/app", "1"]

  config.vm.provision :chef_solo do |chef|
    chef.add_recipe "nodejs"
    chef.add_recipe "mongodb-debs"
    # chef.add_recipe "redis-server"
    chef.json = {
      "nodejs" => {
        "version" => "0.10.29"
        # uncomment the following line to force
  # recent versions (> 0.8.5) to be built from
  # the source code
  # , "from_source" => true
      }
    }
  end

  config.vm.provision :shell, :inline => "sudo apt-get install -y build-essential --no-install-recommends"
  config.vm.provision :shell, :inline => "sudo apt-get install -y redis-server --no-install-recommends"
  config.vm.provision :shell, :inline => "sudo apt-get install -y ruby1.9.1-dev --no-install-recommends"
  config.vm.provision :shell, :inline => "sudo apt-get install -y ruby1.9.3 --no-install-recommends"
  config.vm.provision :shell, :inline => "sudo gem install cf"
end
