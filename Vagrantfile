# Base Image
BOX_IMAGE = "ubuntu/focal64"
BOX_VERSION = "20220314.0.0"

# max number of worker nodes
N = 2
# Version : Ex) k8s_V = '1.22.7'
k8s_V = '1.23.4'
calico_V = '3.21.4'
lab_N = "Calico-k8s"

Vagrant.configure("2") do |config|
#-----Router Node
    config.vm.define "k8s-rtr" do |subconfig|
      subconfig.vm.box = BOX_IMAGE
      subconfig.vm.box_version = BOX_VERSION
      subconfig.vm.provider "virtualbox" do |v|
        v.customize ["modifyvm", :id, "--groups", "/Calico-Lab"]
        v.name = "Calico-k8s-rtr"
        v.memory = 512
        v.cpus = 1
        v.linked_clone = true
      end
      subconfig.vm.hostname = "k8s-rtr"
      subconfig.vm.synced_folder "./", "/vagrant", disabled: true
      subconfig.vm.network "private_network", ip: "192.168.10.254"
      subconfig.vm.network "private_network", ip: "192.168.20.254"
      subconfig.vm.network "forwarded_port", guest: 22, host: 50000, auto_correct: true, id: "ssh"
      subconfig.vm.provision "shell", path: "https://raw.githubusercontent.com/gasida/KANS/main/3/linux_router.sh" 
    end

#-----Manager Node
    config.vm.define "k8s-m" do |subconfig|
      subconfig.vm.box = BOX_IMAGE
      subconfig.vm.box_version = BOX_VERSION
      subconfig.vm.provider "virtualbox" do |v|
        v.customize ["modifyvm", :id, "--groups", "/Calico-Lab"]
        v.customize ["modifyvm", :id, "--nicpromisc2", "allow-all"]
        v.name = "Calico-k8s-m"
        v.memory = 2048
        v.cpus = 2
        v.linked_clone = true
      end
      subconfig.vm.hostname = "k8s-m"
      subconfig.vm.synced_folder "./", "/vagrant", disabled: true
      subconfig.vm.network "private_network", ip: "192.168.10.10"
      subconfig.vm.network "forwarded_port", guest: 22, host: 50010, auto_correct: true, id: "ssh"
      subconfig.vm.provision "shell", path: "https://raw.githubusercontent.com/gasida/KANS/main/3/init_cfg.sh", args: [ N, k8s_V, calico_V ]
      subconfig.vm.provision "shell", path: "https://raw.githubusercontent.com/gasida/KANS/main/3/route1.sh"
      subconfig.vm.provision "shell", path: "https://raw.githubusercontent.com/gasida/KANS/main/3/master.sh", args: [ N, k8s_V, calico_V, lab_N ]
    end

#-----Worker Node Subnet2
    config.vm.define "k8s-w0" do |subconfig|
      subconfig.vm.box = BOX_IMAGE
      subconfig.vm.box_version = BOX_VERSION
      subconfig.vm.provider "virtualbox" do |v|
        v.customize ["modifyvm", :id, "--groups", "/Calico-Lab"]
        v.customize ["modifyvm", :id, "--nicpromisc2", "allow-all"]
        v.name = "Calico-k8s-w0"
        v.memory = 1536
        v.cpus = 2
        v.linked_clone = true
      end
      subconfig.vm.hostname = "k8s-w0"
      subconfig.vm.synced_folder "./", "/vagrant", disabled: true
      subconfig.vm.network "private_network", ip: "192.168.20.100"
      subconfig.vm.network "forwarded_port", guest: 22, host: 50020, auto_correct: true, id: "ssh"
      subconfig.vm.provision "shell", path: "https://raw.githubusercontent.com/gasida/KANS/main/3/init_cfg.sh", args: [ N, k8s_V, calico_V ]
      subconfig.vm.provision "shell", path: "https://raw.githubusercontent.com/gasida/KANS/main/3/route2.sh"
      subconfig.vm.provision "shell", path: "https://raw.githubusercontent.com/gasida/KANS/main/3/worker.sh", args: [ N, k8s_V, calico_V ]
    end

#-----Worker Node Subnet1
  (1..N).each do |i|
    config.vm.define "k8s-w#{i}" do |subconfig|
      subconfig.vm.box = BOX_IMAGE
      subconfig.vm.box_version = BOX_VERSION
      subconfig.vm.provider "virtualbox" do |v|
        v.customize ["modifyvm", :id, "--groups", "/Calico-Lab"]
        v.customize ["modifyvm", :id, "--nicpromisc2", "allow-all"]
        v.name = "Calico-k8s-w#{i}"
        v.memory = 1536
        v.cpus = 2
        v.linked_clone = true
      end
      subconfig.vm.hostname = "k8s-w#{i}"
      subconfig.vm.synced_folder "./", "/vagrant", disabled: true
      subconfig.vm.network "private_network", ip: "192.168.10.10#{i}"
      subconfig.vm.network "forwarded_port", guest: 22, host: "5001#{i}", auto_correct: true, id: "ssh"
      subconfig.vm.provision "shell", path: "https://raw.githubusercontent.com/gasida/KANS/main/3/init_cfg.sh", args: [ N, k8s_V, calico_V ]
      subconfig.vm.provision "shell", path: "https://raw.githubusercontent.com/gasida/KANS/main/3/route1.sh"
      subconfig.vm.provision "shell", path: "https://raw.githubusercontent.com/gasida/KANS/main/3/worker.sh", args: [ N, k8s_V, calico_V ]
    end
  end

end