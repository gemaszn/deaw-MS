
Vagrant.configure("2") do |config|
  config.vm.box = "debian/bookworm64"
  config.vm.provision "shell", inline: <<-SHELL
     apt-get update
     apt-get install -y bind9
   SHELL

  config.vm.define "tierra" do |tierra|
    tierra.vm.network "private_network", ip: "192.168.57.103"
    tierra.vm.hostname = "tierra.sistema.test"

    tierra.vm.provision "shell", name: "dns-master", inline: <<-SHELL
      cp -v /vagrant/named.conf.options /etc/bind/
      cp -v /vagrant/named.conf.localmaster /etc/bind/named.conf.local
      cp -v /vagrant/sistema.test.dns /var/lib/bind/
      cp -v /vagrant/192.168.57.dns /var/lib/bind/
      cp -v /vagrant/resolv.conf /etc/resolv.conf
      systemctl reload named
      systemctl status named
    SHELL
  end

  config.vm.define "venus" do |venus|
    venus.vm.network "private_network", ip: "192.168.57.102"
    venus.vm.hostname = "venus.sistema.test"

    venus.vm.provision "shell", name: "dns-slave", inline: <<-SHELL
      cp -v /vagrant/named.conf.options /etc/bind/
      cp -v /vagrant/named.conf.localslave /etc/bind/named.conf.local
      cp -v /vagrant/resolv.confslave /etc/resolv.conf
      systemctl reload named
      systemctl status named
    SHELL
  end

  
end
