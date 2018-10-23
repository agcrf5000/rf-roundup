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

## 2. Install NodeJS

#### 1. SSH into VM
`> vagrant ssh`

#### 2. Install NodeJS
`> sudo apt-get update && sudo apt-get upgrade`

`> cd ~`

`> curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -`

`> sudo apt-get install -y nodejs`

`> sudo apt-get install build-essential`

---

## 3. Install Yarn

#### 1. Npm Yarn
`> sudo npm install -g yarn`

---

## 4. Setup Firebase

#### 1. Create an NPM global folder
[How to Prevent Permissions Errors](https://docs.npmjs.com/getting-started/fixing-npm-permissions)

#### 1. Install Firebase
`> sudo npm install -g firebase-tools`

#### 2. Login
`> firebase login:ci --no-localhost`

4/AADdLthczYb7QH1QKtu-5M4QXatNMZEbxmov1O_0gzfsyV4vRvPS3O8

Goto URL and get code to paste into terminal. This should login you in. If not, try again.

---

##3 5. Create Firebase project

#### 1. Firebase init
`> firebase init`

Do not install dependencies using npm. Use Yarn.
