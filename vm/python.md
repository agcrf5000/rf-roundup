# VM Environment Setup

_Average time to complete setup: 2 hrs._

Requirements:
  * [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
  * [Vagrant](https://www.vagrantup.com/downloads.html)
  * [Git](https://git-scm.com/downloads)

References:
  * [Pyton3 on Ubuntu Server 16](https://www.digitalocean.com/community/tutorials/how-to-install-python-3-and-set-up-a-programming-environment-on-an-ubuntu-16-04-server)
  * [Pyton3 on Ubuntu 16](https://www.digitalocean.com/community/tutorials/how-to-install-python-3-and-set-up-a-local-programming-environment-on-ubuntu-16-04)
  * [Redis on Ubuntu 16](https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-redis-on-ubuntu-16-04)
  * [Install TensorFlow](https://www.tensorflow.org/install/install_linux)

---

## 1. Install Ubuntu

#### 1. Create new project folder
Use Windows File Explore to create a new project folder. Then 'right-click' folder, select 'GIT Bash Here'

#### 2. Add Ubuntu/bionic64 VagrantBox
`> vagrant box add ubuntu/bionic64`

#### 3. Initialize
`> vagrant init ubuntu/bionic64`

`> vagrant up`

#### 4. Vagrant-VBGuest plugin

`> vagrant halt`

`> vagrant plugin install vagrant-vbguest`

`> vagrant reload`

---

## 2. Install Python

#### 1. SSH into VM
`> vagrant ssh`

#### 2. SSH into VM
`> sudo apt-get update`

`> sudo apt-get -y upgrade`

`> sudo apt-get -y upgrade`

`> sudo apt-get install python3-pip python3-dev python-virtualenv`

`> sudo apt-get install python-setuptools`

---

## 3. Setup Python VirtualEnv (VE) w/ TensorFlow

#### 1. Create VE
`> sudo virtualenv --system-site-packages -p python3 ~/tensorflow`

#### 2. Activate VE
`> source ~/tensorflow/bin/activate`

#### 3. Install TensorFlow in VE
`> pip3 install --upgrade tensorflow`

#### 4. Test TensFlow
[TensorFlow - Validate your installation](https://www.tensorflow.org/install/install_linux#ValidateYourInstallation)
