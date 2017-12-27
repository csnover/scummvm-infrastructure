Vagrant.configure("2") do |config|

  config.vm.define "ansible" do |ansible|
    ansible.vm.box = "debian/contrib-stretch64"
    ansible.vm.network "private_network", ip: "192.168.10.100"

    ansible.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y python-pip
      pip install ansible
SHELL

    ansible.vm.provision "shell", privileged: false, inline: <<-SHELL
      echo "[defaults]
host_key_checking = False

[ssh_connection]
pipelining = True" > ~/.ansible.cfg
SHELL

    ansible.vm.provision "shell", privileged: false, inline: <<-SHELL
      ssh-keygen -N "" -f ~/.ssh/id_rsa -q
      cp ~/.ssh/id_rsa.pub /vagrant/vagrant.pub
SHELL

  end

  config.vm.define "vm1" do |vm1|
    vm1.vm.box = "debian/contrib-stretch64"
    vm1.vm.network "private_network", ip: "192.168.10.2"
  end

  config.vm.define "vm2" do |vm2|
    vm2.vm.box = "debian/contrib-jessie64"
    vm2.vm.network "private_network", ip: "192.168.10.3"
  end

  (1..2).each do |i|
    config.vm.define "vm#{i}" do |node|
      node.vm.provision "shell", privileged: false, inline: "cat /vagrant/vagrant.pub >> ~/.ssh/authorized_keys"
    end
  end
end
