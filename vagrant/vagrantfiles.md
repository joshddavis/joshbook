# Vagrant Files
Vagrant files control how the box and environment are provisioned. By running the init command on the prior page, a vagrant file will be generated in the working directory if one doesn't already exist.

<br/>

#### Main Parts of a Vagrant File
* **config.vm.box** - operating system

* **config.vm.provider** - virtualbox

* **config.vm.network** - how host computer sees your box

* **config.vm.synced_folder** - how you access files from your computer

* **config.vm.provision** - what we want set up (lamp, mean, etc..)

<br/>

#### Vagrant File Example
The below example shows a vagrant file that points to a separate bootstrap.sh file used for provisioning the box.

```
# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|

  # Box Settings
  config.vm.box = "ubuntu/trusty64"

  # Provider Settings
  config.vm.provider "virtualbox" do |vb|
    vb.memory = 2048
    vb.cpus = 2
  end

  # Network Settings
  # config.vm.network "forwarded_port", guest: 80, host: 8080
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"
  config.vm.network "private_network", ip: "192.168.33.10"
  # config.vm.network "public_network"

  # Folder Settings
  config.vm.synced_folder ".", "/var/www/html", :mount_options => ["dmode=777","fmode=666"]

  # Provision Settings
  config.vm.provision "shell", path: "bootstrap.sh"

  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL

end
```
