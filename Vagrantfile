
$WEB_PROJECT_FOLDER = "WebProject"

Vagrant.configure("2") do |config|
  config.vm.box = "vagrant-mono"
  config.vm.box_url = "https://github.com/chilimangoes/vagrant-mono/releases/download/3.2.3/package.box"
  #config.vm.box_url = "https://atlas.hashicorp.com/ubuntu/boxes/trusty64/versions/20150609.0.10/providers/virtualbox.box"

  config.vm.provider :virtualbox do |vb|
    # Use VBoxManage to customize the VM. For example to change memory:
    vb.customize ["modifyvm", :id, "--memory", "2048"]
  end

  config.vm.provision :shell, :path => "build-support/provisioning/install-nginx.sh"
  config.vm.provision :shell, :path => "build-support/provisioning/install-fastcgi-mono.sh"
  config.vm.provision :shell, :path => "build-support/provisioning/configure-nginx.sh"
  config.vm.provision :shell, :path => "build-support/provisioning/configure-fastcgi-mono.sh"
  config.vm.provision :shell, :path => "build-support/provisioning/tools.sh"

  config.vm.provision :shell, :path => "build-support/provisioning/configure-website-dev.sh", args: $WEB_PROJECT_FOLDER
  #config.vm.synched_folder "/vagrant/src/WebProject/", "/var/wwwroot/"
  #config.mount_commands.command "sudo mount --bind /vagrant/src/" + $WEB_PROJECT_FOLDER + "/ /var/wwwroot/"
  config.vm.network :forwarded_port, guest: 80, host: 8093
end
