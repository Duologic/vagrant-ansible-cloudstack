# -*- mode: ruby -*-
# vi: set ft=ruby :

ENV['VAGRANT_DEFAULT_PROVIDER'] = 'libvirt'

Vagrant.configure("2") do |config|
   config.vm.box = "centos/7"

   ansible_groups = {
   }
   ansible_extra_vars = {
   }


    config.vm.define "cloudstack" do |machine|
        machine.vm.provider "libvirt" do |v|
            v.memory = 2048
        end
        machine.vm.hostname = "cloudstack"
        machine.vm.network "forwarded_port", guest: 8080, host: 8080
        machine.vm.provision :ansible do |ansible|
            ansible.groups = ansible_groups
            ansible.limit = "all"
            ansible.playbook = "cloudstack.yml"
            ansible.extra_vars = ansible_extra_vars
        end
    end

    config.vm.define "cloudstack-agent" do |machine|
        machine.vm.provider "libvirt" do |v|
            v.memory = 2048
        end
        machine.vm.hostname = "cloudstack-agent"
    end


    config.vm.provision "shell", inline: <<-SHELL
        yum install -y epel-release
        yum install -y htop vim telnet curl
    SHELL
end
