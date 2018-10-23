# VM Environment Setup

_Average time to complete setup: 2 hrs._

Requirements:
  * [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
  * [Vagrant](https://www.vagrantup.com/downloads.html)
  * [Git](https://git-scm.com/downloads)

References:
  * [Install Nginx on Ubuntu 16.04](https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-16-04)
  * [Node.js Application for Production on Ubuntu](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-node-js-application-for-production-on-ubuntu-16-04)
  * [NodeSource Node.js Binary Distributions](https://github.com/nodesource/distributions)

---

## 1. Install Ubuntu

#### 1. Create new project folder
Use Windows File Explore to create a new project folder. Then 'right-click' folder, select 'GIT Bash Here'

#### 2. Add Ubuntu/Xenial64 VagrantBox
`> vagrant box add ubuntu/xenial64`

#### 3. Initialize
`> vagrant init ubuntu/xenial64`

`> vagrant up`

#### 4. Vagrant-VBGuest plugin

`> vagrant halt`

`> vagrant plugin install vagrant-vbguest`

`> vagrant reload`

---

## 2. Install Nginx

#### 1. SSH into VM
`> vagrant ssh`

#### 2. Install Nginx
`> sudo apt-get update && sudo apt-get upgrade`

`> sudo apt-get -y install nginx`

`> sudo service nginx start`

---

## 3. Install NodeJS

#### 1. SSH into VM
`> vagrant ssh`

#### 2. Install NodeJS
`> sudo apt-get update && sudo apt-get upgrade`

`> cd ~`

`> curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -`

`> sudo apt-get install -y nodejs`

`> sudo apt-get install build-essential`

---

## 3. Install PM2

#### 1. SSH into VM
`> vagrant ssh`

#### 2. Install PM2
`> sudo npm install -g pm2`

`> pm2 start [application name]`

`> pm2 startup systemd`

`> sudo env PATH=$PATH:/usr/bin /usr/lib/node_modules/pm2/bin/pm2 startup systemd -u vagrant --hp /home/vagrant`

`> systemctl status pm2-vagrant`

---

## 4. Set Up Nginx as a Reverse Proxy Server

`> sudo nano /etc/nginx/sites-available/default`
