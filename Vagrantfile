# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.vm.synced_folder ".", "/vagrant", type: "rsync", 
    rsync__exclude: [".git/","es_archive","kb_archive","ls_archive","fb_archive","jdk","datasets"]
  config.vm.provision "shell", path: "provision_privileged.sh", privileged: true
  
  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.memory = "1024"
  end

  config.vm.define "node1" do |node1|
    node1.vm.provider "virtualbox" do |v|
      v.name = "Elastic Lab Node 1"
	  v.memory = "2048"
    end
	node1.vm.provision "file", source: "es_archive", destination: "/home/vagrant"
    node1.vm.provision "shell", path: "provision_elasticsearch.sh", privileged: false
	
	node1.vm.provision "file", source: "ls_archive", destination: "/home/vagrant"
	node1.vm.provision "file", source: "fb_archive", destination: "/home/vagrant"
	node1.vm.provision "file", source: "jdk", destination: "/home/vagrant/jdk"
	node1.vm.provision "file", source: "datasets", destination: "/home/vagrant/datasets"
	node1.vm.provision "shell", path: "provision_datasets.sh", privileged: false
    node1.vm.network "private_network", ip: "10.0.200.101"
    node1.vm.hostname = "node1"
  end

  # config.vm.define "node2" do |node2|
  #   node2.vm.provider "virtualbox" do |v|
  #     v.name = "Elastic Lab Node 2"
  #   end
  #   node2.vm.provision "file", source: "es_archive", destination: "/home/vagrant"
  #   node2.vm.provision "shell", path: "provision_elasticsearch.sh", privileged: false
  #   node2.vm.network "private_network", ip: "10.0.200.102"
  #   node2.vm.hostname = "node2"
  # end

  # config.vm.define "node3" do |node3|
  #   node3.vm.provider "virtualbox" do |v|
  #     v.name = "Elastic Lab Node 3"
  #   end
  #   node3.vm.provision "file", source: "es_archive", destination: "/home/vagrant"
  #   node3.vm.provision "shell", path: "provision_elasticsearch.sh", privileged: false
  #   node3.vm.network "private_network", ip: "10.0.200.103"
  #   node3.vm.hostname = "node3"
  # end
  
  # config.vm.define "node4" do |node4|
  #   node4.vm.provider "virtualbox" do |v|
  #     v.name = "Elastic Lab Node 4"
  #   end
  #   node4.vm.provision "file", source: "es_archive", destination: "/home/vagrant"
  #   node4.vm.provision "shell", path: "provision_elasticsearch.sh", privileged: false
  #   node4.vm.network "private_network", ip: "10.0.200.104"
  #   node4.vm.hostname = "node4"
  # end

  # config.vm.define "node5" do |node5|
  #   node5.vm.provider "virtualbox" do |v|
  #     v.name = "Elastic Lab Node 5"
  #   end
  #   node5.vm.provision "file", source: "es_archive", destination: "/home/vagrant"
  #   node5.vm.provision "shell", path: "provision_elasticsearch.sh", privileged: false
  #   node5.vm.network "private_network", ip: "10.0.200.105"
  #   node5.vm.hostname = "node5"
  # end
  
  # config.vm.define "node6" do |node6|
  #   node6.vm.provider "virtualbox" do |v|
  #     v.name = "Elastic Lab Node 6"
  #   end
  #   node6.vm.provision "file", source: "es_archive", destination: "/home/vagrant"
  #   node6.vm.provision "shell", path: "provision_elasticsearch.sh", privileged: false
  #   node6.vm.network "private_network", ip: "10.0.200.106"
  #   node6.vm.hostname = "node6"
  # end

  # config.vm.define "node7" do |node7|
  #   node7.vm.provider "virtualbox" do |v|
  #     v.name = "Elastic Lab Node 7"
  #   end
  #   node7.vm.provision "file", source: "es_archive", destination: "/home/vagrant"
  #   node7.vm.provision "shell", path: "provision_elasticsearch.sh", privileged: false
  #   node7.vm.network "private_network", ip: "10.0.200.107"
  #   node7.vm.hostname = "node7"
  # end

  config.vm.define "nodekb" do |nodekb|
    nodekb.vm.provider "virtualbox" do |v|
      v.name = "Elastic Lab Kibana"
    end
	nodekb.vm.provision "file", source: "kb_archive", destination: "/home/vagrant"
    nodekb.vm.provision "shell", path: "provision_kibana.sh", privileged: false
    nodekb.vm.network "private_network", ip: "10.0.200.110"
    nodekb.vm.hostname = "nodekb"
  end

end
