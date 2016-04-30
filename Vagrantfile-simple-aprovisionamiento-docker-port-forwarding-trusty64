# -*- mode: ruby -*-
# vi: set ft=ruby :

# Specify Vagrant version and Vagrant API version
Vagrant.require_version ">= 1.6.0"
VAGRANTFILE_API_VERSION = "2"
ENV['VAGRANT_DEFAULT_PROVIDER'] = 'docker'

DOCKER_HOST_NAME = "dockerhost"
DOCKER_HOST_VAGRANTFILE = "./DockerHostVagrantfile"

MYSQL_ROOT_PASSWORD="root"

# Create and configure the Docker container(s)
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.vm.define "00mysql" do |v|
    v.vm.provider "docker" do |d|
      d.force_host_vm = 'true'
      d.vagrant_vagrantfile = "#{DOCKER_HOST_VAGRANTFILE}"
      d.remains_running = 'true'
      d.image = "mysql:5.7.9"
      d.env = { :MYSQL_ROOT_PASSWORD => MYSQL_ROOT_PASSWORD }
      d.ports = ['3306:3306']
      d.name = '00mysql-container'
    end
  end

  config.vm.define "drupal" do |v|
    v.vm.provider "docker" do |d|
      d.force_host_vm = 'true'
      d.vagrant_vagrantfile = "#{DOCKER_HOST_VAGRANTFILE}"
      d.remains_running = 'true'
      d.image = "drupal"
      d.ports = ['80:80']
      d.name = 'drupalx-container'
#      d.link("00mysql-container:mysql")
    end
  end

end
