
Vagrant.configure("2") do |config|
  config.vm.box = "debian/bookworm64"
  config.vm.provision "shell", inline: <<-SHELL
     apt-get update
     apt-get install -y bind9
   SHELL

  config.vm.define "tierra" do |tierra|
    tierra.vm.network "private network", ip: "192.168.57.103"
    tierra.vm.hostname = "tierra.sistema.test"
  end

  config.vm.define "venus" do |venus|
    venus.vm.network "private network", ip: "192.168.57.102"
    venus.hostname = "venus.sistema.test"
  end

  
end
