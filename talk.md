class: center, middle

# Vagrant

![Solr Logo](http://www.vagrantup.com/images/vagrant_header_background-482a12a7.png)

Toby Cole, Technical Architect, Semantico

---

# What am I talking about?

* What is Vagrant
* Installing 
* Starting
* Configuring
* Use-cases

---

# What is vagrant?

* VM management layer
* Designed for devs
* Portable, disposable images
* Multiple VM providers (virtualbox, VMware, AWS…)
* Shareable config (can be checked into projects!)

---


# Installation (easy way)

    ➜  ~  brew cask install vagrant
    
---
    
# Installation (hard way)

![Download installer](download.png)

---

# First VM

    ➜  ~  vagrant init precise32 http://files.vagrantup.com/precise32.box
    ➜  ~  vagrant up
    
Lets go!

---

# More commands

    ➜  ~  vagrant ssh
    ➜  ~  vagrant destroy

---

# Don't 'rm -rf /'

* Current directory is mounted on /vagrant
* Handy since you have a known path to your project
* It's **writable**

---

# Config is ruby

    ➜  ~  cat Vagrantfile
    Vagrant.configure("2") do |config|
        config.vm.box = "precise32"
    end

---

# Provisioning

* Get stuff installed when you `vagrant up`
* Many built in providers
   * shell scripts
   * puppet
   * ansible
   * chef
   * docker
   * salt
   
---

# Shell script example

## bootstrap.sh

    #!/usr/bin/env bash

    apt-get update
    apt-get install -y apache2
    rm -rf /var/www
    ln -fs /vagrant /var/www
    
## Vagrantfile

    Vagrant.configure("2") do |config|
      config.vm.box = "precise32"
      config.vm.provision :shell, :path => "bootstrap.sh"
    end
    
## Go
    vagrant reload --provision
    
Not yet accessible outside of the VM…

---

# Port forwarding
One line in your Vagrantfile

    config.vm.network :forwarded_port, host: 4567, guest: 80

Then a `vagrant reload`

---

# Other stuff!
* Multiple VMs in one file
* LXC containers! - ask Nico
* Easy per-dev puppetmasters with Ansible & Vagrant - ask RobW
* Plugins - most components of vagrant are pluggable, written in Ruby. 
* See [http://docs.vagrantup.com](http://docs.vagrantup.com), very nice docs.
* 
---

class: center, middle
# Questions‽
