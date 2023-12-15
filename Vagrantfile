Vagrant.configure("2") do |config|

    config.vm.define "master" do |master|
      master.vm.box = "ubuntu/bionic64"
      master.vm.network "private_network", type: "dhcp"
      master.vm.network "forwarded_port", guest: 2377, host: 2377
      master.vm.network "forwarded_port", guest: 7946, host: 7946
      master.vm.network "forwarded_port", guest: 4789, host: 4789
      master.vm.hostname = "master"
      master.vm.provider "virtualbox" do |vb|
        vb.memory = "1024"
        vb.cpus = 1
      end
      master.vm.provision "shell", inline: <<-SHELL
        sudo apt-get update
        sudo apt-get install -y docker.io
        sudo usermod -aG docker vagrant
      SHELL
    end

    ["node01", "node02", "node03"].each do |node_name|
      config.vm.define node_name do |node|
        node.vm.box = "ubuntu/bionic64"
        node.vm.network "private_network", type: "dhcp"
        node.vm.hostname = node_name
        node.vm.provider "virtualbox" do |vb|
          vb.memory = "512"
          vb.cpus = 1
        end
        node.vm.provision "shell", inline: <<-SHELL
          sudo apt-get update
          sudo apt-get install -y docker.io
          sudo usermod -aG docker vagrant
        SHELL
      end
    end
end
  