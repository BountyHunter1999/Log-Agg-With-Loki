Vagrant.configure("2") do |config|

  config.vm.box = "adhikarishrish1/Swarm-ubuntu-2004"
  config.vm.box_version = "1.0.2"

  config.vm.define "main" do |app|
    app.vm.hostname = "swarm-main"
    app.vm.synced_folder "./provisioner", "/home/vagrant/provisioner"
    app.vm.network :private_network, ip: "192.168.57.2"
    config.vm.provision "shell", inline: <<-SHELL
      apt-get update -y
      apt-get upgrade -y
      apt install ansible -y
      ssh-keygen -t rsa -b 4096 -N '' -f '/home/vagrant/.ssh/id_rsa'
      apt install sshpass -y
    SHELL
  end

  
  (3..4).each do |i|
    config.vm.define "server#{i - 2}" do |app|
    app.vm.hostname = "swarm-node#{i - 2}"
    app.vm.synced_folder ".", "/vagrant", disabled: true
    # app.vm.network "private_network", type: "dhcp"
    app.vm.network "private_network", ip: "192.168.57.#{i}"
    app.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
    end
  end
end

end
