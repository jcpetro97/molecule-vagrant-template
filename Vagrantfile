# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
    boxes = [
      { :name => "template-ubuntu2004", :box => "jcpetro97/ubuntu2004" },
      { :name => "template-ubuntu1804", :box => "jcpetro97/ubuntu1804" }
      { :name => "template-centos7", :box => "jcpetro97/centos7" }
      { :name => "template-centos8", :box => "jcpetro97/centos8" }
    ]
    config.vm.provider "virtualbox" do |v|  
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
    end      
    boxes.each do |opts|
      config.vm.define opts[:name] do |config|
        config.vm.box = opts[:box]
        if opts[:name] == boxes.last[:name]
          config.vm.provision "ansible" do |ansible|
            ansible.playbook = "test.yml"
            ansible.verbose = "v"
            ansible.limit = "all"
          end
        end
      end
    end
  end
