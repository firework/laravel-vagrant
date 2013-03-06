# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant::Config.run do |config|
  config.vm.box     = 'precise32'
  config.vm.box_url = 'http://files.vagrantup.com/precise32.box'
  
  # Tell the VM to use UTC.
  # @see http://www.virtualbox.org/manual/ch03.html#settings-motherboard
  config.vm.customize ['modifyvm', :id, '--rtcuseutc', 'on']

  # UTC ALL THE THINGS!
  # @see http://www.xormedia.com/utc-is-the-only-real-timezone/
  config.vm.provision :shell, :inline => 'echo "Etc/UTC" | sudo tee /etc/timezone && dpkg-reconfigure --frontend noninteractive tzdata'

  # Assign this VM to a host-only network IP, allowing you to access it
  # via the IP. Host-only networks can talk to the host machine as well as
  # any other machines on the same network, but cannot be accessed (through this
  # network interface) by any external networks.
  config.vm.network :hostonly, '33.33.33.33'

  config.vm.forward_port 80, 8888
  config.vm.forward_port 3306, 8889

  # Share an additional folder to the guest VM. The first argument is
  # an identifier, the second is the path on the guest to mount the
  # folder, and the third is the path on the host to the actual folder.
  # config.vm.share_folder "v-data", "/vagrant_data", "../data"

  config.vm.provision :puppet do |puppet|
    puppet.manifests_path = 'puppet/manifests'
    puppet.manifest_file  = 'base.pp'
    puppet.module_path    = 'puppet/modules'
  end
end
