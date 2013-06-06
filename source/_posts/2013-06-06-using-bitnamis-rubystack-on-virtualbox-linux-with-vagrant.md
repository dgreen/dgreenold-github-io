---
layout: post
title: "Using Bitnami's Rubystack on VirtualBox Linux with Vagrant"
date: 2013-06-06 01:36
comments: true
categories: developer
---

In my Software Engineering Projects class, we are going to do a RAILS-based
project.  Based on feedback from last year's class, I am furnishing students
with an almost configured RAILS system for development.  The system is based on

  * [Bitnami's Rubystack for 32 bit Linux][4046-001]
  * [VirtualBox 4.2.12][4046-002] as the VM
  * [Vagrant 1.22][4046-003] to help manage the install
  * [Ubuntu precise32][4046-004] Linux

## Create the base machine

The `Vagrantfile` is configured to support networking from the host machine
and to run a configuration script (`script.sh`) as part of the provisioning.
There is a small bit of logic to avoid re-provisioning things each time the
machine is brought up.

I make it by following roughly the following procedure:

  1. Install Virtualbox
  1. Install Vagrant
  1. Create a directory to place files add in
    * The bitnami linux installer file
    * `Vagrantfile`
    * `script.sh`
  1. Do an install:  `vagrant up`
  1. SSH into the running host:  `vagrant ssh`
  1. Use Linux as needed
  1. Exit back to the host OS:  `exit`
  1. Shutdown the virtual machine (saving the contents):  `vagrant halt`
  1. Package the machine post configuration with `vagrant package default --output rails3r2e13.box`

  1. Restart the machine and continue work:  `vagrant up`

## Install the base machine on student computer ##

OS X/Linux commands are given here, make appropriate changes for Windows.

  1. Create a vms directory for your development use `mkdir vms`
  1. Create a machine1 directory `mkdir vms/machine1`  It will be accessible to both
     Linux and your operating system.
  1. `cd vms/machine1`
  1. `vagrant init rails3r2e13.box https://dl.dropboxusercontent.com/u/4214925/vms/rails3r2e13.box`
  1. uncomment `config.vm.network :private_network, ip: "192.168.33.10"` in Vagrantfile
  1. `vagrant up`              # first time will download the vm machine
  1. `vagrant ssh`             # if this fails, you need to put SSH on the path

## SSH for Windows ##

Windows does not include SSH by default.  Two options are to 1) install Git locally and then use it's SSH implementation and 2) [install PuTTY][putty].

## Limitations ##

The file `.bashrc` has a line at the end of it that maps the rails commands onto
the path along with library linkage as well.  This messes up some local commands
`nano` and others.  One solution is to comment out the line and re-log into the
VM.


## Other vagrant commands

  * `vagrant destroy`  eliminate the virtual machine so next time it will be rebuilt
  * `vagrant reload`  combination of of halt then up
  * `vagrant suspend` pause machine copying state to disk, resume with `vagrant resule``

{% codeblock Vagrantfile lang:ruby %}
 -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "precise32"
  config.vm.box_url = "http://files.vagrantup.com/precise32.box"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network :private_network, ip: "192.168.33.10"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  config.vm.provision :shell, :path => "script.sh"

end
{% endcodeblock %}


{% codeblock script.sh lang:bash %}
#!/usr/bin/env bash

set -e      # Exit script on error
set -x      # Print commands and arguments

echo "Starting configuration script"

# Abort provisioning if rubystack is already installed.
test -d /opt/rubystack-1.9.3-10 &&
{ echo "rubystack already installed."; exit 0; } 

echo "Provisioning rubystack from bitnami"

# Install bitnami
/vagrant/bitnami-rubystack-1.9.3-10-linux-installer.run --mode unattended \
                                  --disable-components varnish,phpmyadmin,rvm

# install the quiet_assets gem
gem install quiet_assets -f --install-dir /opt/rubystack-1.9.3-10/ruby/lib/ruby/gems/1.9.1 

# make vagrant user owner of the install
chown -R vagrant.vagrant /opt/rubystack-1.9.3-10

# install a symbolic link to rubystack directory
ln -s /opt/rubystack-1.9.3-10 /home/vagrant/rubystack

# put ruby / rails code on path
echo ". /opt/rubystack-1.9.3-10/scripts/setenv.sh" >> /home/vagrant/.bashrc

echo "Provisioning complete."
{% endcodeblock %}







[4046-001]: http://bitnami.com/stack/ruby "Ruby Stack Cloud Hosting, Installers and Virtual Machines. - BitNami"
[4046-002]: https://www.virtualbox.org/ "Oracle VM VirtualBox"
[4046-003]: http://www.vagrantup.com/ "Vagrant"
[4046-004]: http://releases.ubuntu.com/precise/ "Ubuntu 12.04.2 LTS (Precise Pangolin) - Ubuntu Releases"
[putty]: http://docs-v1.vagrantup.com/v1/docs/getting-started/ssh.html
