Vagrant.configure("2") do |config|
  config.vm.define "server" do |control_plane|
    control_plane.vm.box = "ubuntu/trusty64"

    # Disable automatic box update checking. If you disable this, then boxes will only be checked for updates 
    # when the user runs `vagrant box outdated`. This is not recommended.
    control_plane.vm.box_check_update = false

    # Create a forwarded port mapping which allows access to a specific port within the machine from a port on the host machine. 
    # In the example below, accessing "localhost:8080" will access port 80 on the guest machine.
    # NOTE: This will enable public access to the opened port
    control_plane.vm.network "forwarded_port", guest: 8080, host: 8082

    # Create a forwarded port mapping which allows access to a specific port  within the machine from a port on the host machine 
    # and only allow access via 127.0.0.1 to disable public access
    # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

    # Create a private network, which allows host-only access to the machine using a specific IP.
    control_plane.vm.network "private_network", type: "static", ip: "192.168.0.10"

    # Create a public network, which generally matched to bridged network.
    # Bridged networks make the machine appear as another physical device on your network.
    # config.vm.network "public_network"

    # Share an additional folder to the guest VM. The first argument is the path on the host to the actual folder. The second 
    # argument is the path on the guest to mount the folder. And the optional third argument is a set of non-required options.
    control_plane.vm.synced_folder "./tomcatwebapps", "/opt/tomcat/webapps"

    # Disable the default share of the current code directory. Doing this provides improved isolation between the vagrant box 
    # and your host by making sure your Vagrantfile isn't accessible to the vagrant box.
    # If you use this you may want to enable additional shared subfolders as shown above.
    # config.vm.synced_folder ".", "/vagrant", disabled: true
    

    # My Provider for Vagrant: 
    control_plane.vm.provider "virtualbox" do |vb| 
      vb.gui = false # Don't display the VirtualBox GUI when booting the machine
      vb.name = "webserver-tomcat" 
      vb.memory = "1024"
    end

    # Enable provisioning with a shell script. Additional provisioners such as
    # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
    # documentation for more information about their specific syntax and use.
    # config.vm.provision "shell", inline: <<-SHELL
    #   apt-get update
    #   apt-get install -y apache2
    # SHELL
  end

  
  config.vm.define "preprodserver" do |preprodwebserver|
    preprodwebserver.vm.box = "bento/ubuntu-22.04"
    preprodwebserver.vm.box_check_update = false
    preprodwebserver.vm.network "forwarded_port", guest: 8080, host: 8083
    preprodwebserver.vm.network "private_network", type: "static", ip: "192.168.0.11"
    preprodwebserver.vm.synced_folder "./srv-tomcatwebapps", "/opt/tomcat/webapps"

    # My Provider for Vagrant: 
    preprodwebserver.vm.provider "virtualbox" do |vb| 
      vb.gui = false # Don't display the VirtualBox GUI when booting the machine
      vb.name = "preprod-webserver" 
      vb.memory = "1024"
    end
  end
end