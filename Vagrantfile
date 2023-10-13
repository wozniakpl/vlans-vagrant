Vagrant.configure("2") do |config|
 
    # Router VM
    config.vm.define "router" do |router|
      router.vm.box = "ubuntu/bionic64"
      router.vm.network "private_network", type: "internal", ip: "192.168.56.1"
  
      router.vm.provision "shell", inline: <<-SHELL
sudo apt-get update
sudo apt-get install -y vlan
sudo modprobe 8021q

# Set up VLAN 10
sudo vconfig add enp0s8 10
sudo ip addr add 192.168.10.1/24 dev enp0s8.10
sudo ip link set up enp0s8.10

# Set up VLAN 20
sudo vconfig add enp0s8 20
sudo ip addr add 192.168.20.1/24 dev enp0s8.20
sudo ip link set up enp0s8.20
SHELL
    end
  
    # NGINX VM (VLAN 10)
    config.vm.define "nginx1" do |nginx|
        nginx.vm.box = "ubuntu/bionic64"
        nginx.vm.network "private_network", type: "internal", ip: "192.168.56.2"
    
        nginx.vm.provision "shell", inline: <<-SHELL
sudo apt-get update
sudo apt-get install -y vlan nginx
sudo modprobe 8021q
sudo vconfig add enp0s8 10
sudo ip addr add 192.168.10.2/24 dev enp0s8.10
sudo ip link set up enp0s8.10
sudo systemctl enable nginx
sudo systemctl start nginx
SHELL
    end
    
    # Client VM 1 (VLAN 10)
    config.vm.define "client1" do |client|
        client.vm.box = "ubuntu/bionic64"
        client.vm.network "private_network", type: "internal", ip: "192.168.56.3"
    
        client.vm.provision "shell", inline: <<-SHELL
sudo apt-get update
sudo apt-get install -y vlan
sudo modprobe 8021q
sudo vconfig add enp0s8 10
sudo ip addr add 192.168.10.3/24 dev enp0s8.10
sudo ip link set up enp0s8.10
SHELL
    end
    
    # NGINX VM (VLAN 20)
    config.vm.define "nginx2" do |nginx|
        nginx.vm.box = "ubuntu/bionic64"
        nginx.vm.network "private_network", type: "internal", ip: "192.168.56.4"
    
        nginx.vm.provision "shell", inline: <<-SHELL
sudo apt-get update
sudo apt-get install -y vlan nginx
sudo modprobe 8021q
sudo vconfig add enp0s8 20
sudo ip addr add 192.168.20.2/24 dev enp0s8.20
sudo ip link set up enp0s8.20
sudo systemctl enable nginx
sudo systemctl start nginx
SHELL
    end
    
    # Client VM 2 (VLAN 20)
    config.vm.define "client2" do |client|
        client.vm.box = "ubuntu/bionic64"
        client.vm.network "private_network", type: "internal", ip: "192.168.56.5"
    
        client.vm.provision "shell", inline: <<-SHELL
sudo apt-get update
sudo apt-get install -y vlan
sudo modprobe 8021q
sudo vconfig add enp0s8 20
sudo ip addr add 192.168.20.3/24 dev enp0s8.20
sudo ip link set up enp0s8.20
SHELL
    end
  
  end
  