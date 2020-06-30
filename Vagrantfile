# -*- mode: ruby -*-
# vi: set ft=ruby :
#
Vagrant.require_version ">= 1.6.0"

boxes = [
    {
        :name => "docker-master",
        :eth1 => "192.168.50.10",
        :mem => "1024",
        :cpu => "1"
    },
    {
        :name => "docker-node1",
        :eth1 => "192.168.50.11",
        :mem => "1024",
        :cpu => "1"
    },
	{
        :name => "docker-node2",
        :eth1 => "192.168.50.12",
        :mem => "1024",
        :cpu => "1"
    }
]

Vagrant.configure(2) do |config|

  config.vm.box = "ubuntu/bionic64"

  boxes.each do |opts|
      config.vm.define opts[:name] do |config|
        config.vm.hostname = opts[:name]

        config.vm.provider "vmware_fusion" do |v|
          v.vmx["memsize"] = opts[:mem]
          v.vmx["numvcpus"] = opts[:cpu]
        end

        config.vm.provider "virtualbox" do |v|
          v.customize ["modifyvm", :id, "--memory", opts[:mem]]
          v.customize ["modifyvm", :id, "--cpus", opts[:cpu]]
        end

        config.vm.network :private_network, ip: opts[:eth1]
      end
  end
  config.vm.provision "shell", privileged: true, path: "./setup.sh"
end
