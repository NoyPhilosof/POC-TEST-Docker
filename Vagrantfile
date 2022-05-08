Vagrant.configure("2") do |config|
    config.vm.box = "ubuntu/bionic64"
    config.vm.hostname = "docker-based"
    config.vm.network "private_network", ip: "192.168.80.80"
    config.vm.synced_folder "./resources/", "/home/vagrant/resources/", create: true
    # config.vm.provision "shell", inline: <<-SHELL
    #   sudo apt-get update
    #   sudo apt-get install software-properties-common
    #   sudo apt-add-repository --yes --update ppa:ansible/ansible
    #   sudo apt-get install ansible --yes
    #   SHELL

    config.vm.provision "shell" do |s|
      ssh_pub_key = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip
      s.inline = <<-SHELL
      echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
      echo #{ssh_pub_key} >> /root/.ssh/authorized_keys
      SHELL
    end

    # config.vm.provision "docker" do |d|
    #   d.pull_images "httpd:latest"
    #   d.pull_images "nginx:latest"
    # end

    config.vm.provider "virtualbox" do |vb|
      vb.memory = "2048"
      vb.cpus = "2"
      vb.name = "Docker-Based"
      # vb.gui = true
    end

#   config.vm.provision "ansible", playbook: "Servers.yml"

  end