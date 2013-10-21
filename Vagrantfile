Vagrant::Config.run do |config|
  config.omnibus.chef_version = "11.4.0"
  config.vm.box = "precise64"
  
  config.vm.forward_port 8000, 8000

  config.vm.share_folder "app", "/home/vagrant/app", "app"

  # allow for symlinks in the app folder
  config.vm.provider :virtualbox do |v, override|
  override.vm.box_url = "http://files.vagrantup.com/precise64.box"
  config.vm.customize ["setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/app", "1"]
  config.vm.customize ["modifyvm", :id, "--memory", 800]
end

  config.vm.provision :chef_solo do |chef|
    chef.cookbooks_path = "cookbooks"
    chef.add_recipe "apt"
    chef.add_recipe "build-essential"
    chef.add_recipe "python"
    chef.add_recipe "apache2"
  end

  # Application provision
  config.vm.provision :shell, :inline => "pip install -r ./app/requirements.txt"

end
