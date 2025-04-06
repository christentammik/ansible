Vagrant.configure("2") do |config|
  config.vm.boot_timeout = 600

  config.vm.define "christen-dockerhost" do |dockerhost|
    dockerhost.vm.box = "generic/debian12"
    dockerhost.vm.network "private_network", ip: "10.10.10.130", netmask: "255.255.255.128"
    dockerhost.vm.hostname = "christen-dockerhost"
    dockerhost.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "8192"]
      vb.customize ["modifyvm", :id, "--cpus", "4"]
      vb.name = "CHRISTEN-DOCKERHOST"
    end
    dockerhost.vm.synced_folder "./docker_data", "/vagrant_data"
    dockerhost.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y snmpd tmux mc wget tree git
      apt-get install -y apt-transport-https ca-certificates curl gnupg-agent software-properties-common
      curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -
      add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable"
      apt-get update
      apt-get install -y docker-ce docker-ce-cli containerd.io
      systemctl enable docker
      systemctl start docker
    SHELL
  end

  config.vm.define "christen-ansible" do |ansible|
    ansible.vm.box = "generic/debian12"
    ansible.vm.network "private_network", ip: "10.10.10.131", netmask: "255.255.255.128"
    ansible.vm.hostname = "christen-ansible"
    ansible.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "8192"]
      vb.customize ["modifyvm", :id, "--cpus", "4"]
      vb.name = "CHRISTEN-ANSIBLE"
    end
    ansible.vm.synced_folder "./ansible_data", "/vagrant_data"
    ansible.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y snmpd tmux mc wget tree git ansible sshpass yamllint ansible-lint
    SHELL
  end

  config.vm.define "christen-ubuntu" do |ubuntu|
    ubuntu.vm.box = "bento/ubuntu-24.04"
    ubuntu.vm.network "private_network", ip: "10.10.10.132", netmask: "255.255.255.128"
    ubuntu.vm.hostname = "christen-ubuntu"
    ubuntu.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "8192"]
      vb.customize ["modifyvm", :id, "--cpus", "4"]
      vb.name = "CHRISTEN-UBUNTU"
    end
    ubuntu.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y snmpd tmux mc wget tree git
    SHELL
  end

  config.vm.define "christen-centos" do |centos|
    centos.vm.box = "generic/centos9s"
    centos.vm.network "private_network", ip: "10.10.10.133", netmask: "255.255.255.128"
    centos.vm.hostname = "christen-centos"
    centos.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "8192"]
      vb.customize ["modifyvm", :id, "--cpus", "4"]
      vb.name = "CHRISTEN-CENTOS"
    end
    centos.vm.provision "shell", inline: <<-SHELL
      yum update -y
      yum install -y net-snmp net-snmp-utils tmux mc wget tree git
    SHELL
  end

  config.vm.define "christen-opensuse" do |opensuse|
    opensuse.vm.box = "bento/opensuse-leap-15"
    opensuse.vm.network "private_network", ip: "10.10.10.134", netmask: "255.255.255.128"
    opensuse.vm.hostname = "christen-opensuse"
    opensuse.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "8192"]
      vb.customize ["modifyvm", :id, "--cpus", "4"]
      vb.name = "CHRISTEN-OPENSUSE"
    end
    opensuse.vm.provision "shell", inline: <<-SHELL
      zypper refresh
	  zypper update -y
      zypper install -y tmux mc wget tree git net-snmp
    SHELL
  end

end
