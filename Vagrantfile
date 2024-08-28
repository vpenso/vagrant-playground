# vi: set ft=ruby :
Vagrant.configure("2") do |config|

  config.vm.provider :libvirt do |libvirt|
    libvirt.memory = 1024
    libvirt.qemu_use_session = false
  end
  
  config.vm.define "alma9" do |node|
    config.vm.box = "almalinux/9"
    config.vm.hostname = "alma9"
    config.vm.network "private_network", ip: "192.168.124.200"
    config.vm.synced_folder ".", "/vagrant", type: "rsync", rsync__exclude: ".git/"
  end

end
