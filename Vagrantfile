# rubocop:disable Naming/FileName
# -*- mode: ruby -*-
# vi: set ft=ruby :

ENV['LANG'] = 'en_US.UTF-8'
ENV['LC_ALL'] = 'en_US.UTF-8'
VAGRANTFILE_DIR = File.dirname(__FILE__)

require "#{VAGRANTFILE_DIR}/vagrant/lib/forklift"

loader = Forklift::BoxLoader.new("#{VAGRANTFILE_DIR}/vagrant")
loader.load!
distributor = Forklift::BoxDistributor.new(loader.boxes)
distributor.distribute!

Vagrant.configure("2") do |config|

    config.vm.define "foreman" do |foreman|


        foreman.vm.hostname = "centos8-katello-devel-stable.example.com"

        foreman.vm.box = "katello/katello-devel"

                foreman.vm.synced_folder "/home/thorben/Projects/katello", "/home/vagrant/katello", type: "sshfs"
        foreman.vm.synced_folder "/home/thorben/Projects/foreman_ansible", "/home/vagrant/foreman_ansible", type: "sshfs"


        foreman.vm.provision "ansible" do |ansible|
            ansible.playbook = 'playbooks/setup_user_devel_environment.yml'

        end

        foreman.vm.provider "libvirt" do |lv|
            #lv.name = "centos8-katello-devel-stable"
            lv.cpus = 8
            lv.memory = 16384
        end

    end


    config.vm.define "smartproxy" do |smartproxy|


        smartproxy.vm.hostname = "smart-proxy-ansible-capable.example.com"

        smartproxy.vm.box = "katello/katello-devel"

        smartproxy.vm.synced_folder "/home/thorben/Projects/smart_proxy_ansible", "/home/vagrant/smart_proxy_ansible", type: "sshfs"
        smartproxy.vm.synced_folder "/home/thorben/Projects/smart-proxy", "/home/vagrant/smart-proxy", type: "sshfs"
        smartproxy.vm.synced_folder "/home/thorben/Projects/smart_proxy_dynflow", "/home/vagrant/smart_proxy_dynflow", type: "sshfs"

        smartproxy.vm.provider "libvirt" do |lv|
            #lv.name = "centos8-smartproxy"
            lv.cpus = 2
            lv.memory = 6144
        end
    end

end


# rubocop:enable Naming/FileName
