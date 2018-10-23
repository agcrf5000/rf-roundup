# VM Environment Setup

_Average time to complete setup: 2 hrs._

Requirements:
  * [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
  * [Vagrant](https://www.vagrantup.com/downloads.html)
  * [Git](https://git-scm.com/downloads)
  * [MySQL Workbench](https://dev.mysql.com/downloads/workbench/)

References:
  * [Install Ubuntu on new VM](https://www.taniarascia.com/what-are-vagrant-and-virtualbox-and-how-do-i-use-them/)
  * [Install Apache, PHP, and MySQL on new VM](https://www.taniarascia.com/how-to-install-apache-php-7-1-and-mysql-on-ubuntu-with-vagrant/)
  * [Setup PHP 7.2 mod_rewrite](https://www.digitalocean.com/community/tutorials/how-to-rewrite-urls-with-mod_rewrite-for-apache-on-ubuntu-16-04)
  * [Vagrantbox Search](https://app.vagrantup.com/boxes/search)

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

## 2. Install Apache

#### 1. SSH into VM
`> vagrant ssh`

#### 2. Install Apache
`> sudo apt-get update && sudo apt-get upgrade`

`> sudo apt-get install apache2 -y`

#### 3. Set servername
`> sudo nano /etc/apache2/apache2.conf`

At the bottom of the apache2.conf file, type:
```
ServerName localhost
```

#### 4. Test setup
`> sudo service apache2 restart`

`> sudo apache2ctl configtest`

`> apache2 -v`

#### 5. Exit VM
`> exit`

---

## 3. Map Domain to IP

#### 1. Edit Vagrantfile
Open Vagrantfile in project folder.

Uncomment:
```
config.vm.network "private_network", ip: "192.168.33.10"
```
Note: The digit in IP address can be used to differentiate domains, per VM.

`> vagrant reload`

#### 2. Edit Hosts File
Open Host file: C:\Windows\System32\drivers\etc\hosts.

Add this code to bottom of file:
```
192.168.33.10  [project name].local
```

#### 3. Test in browser

Goto address: http://[project name].local

---

## 4. Install PHP 7.2

#### 1. SSH into VM
`> vagrant ssh`

#### 2. Install php
`> sudo apt-add-repository ppa:ondrej/php`

`> sudo apt-get update`

`> sudo apt-get install php7.2`

#### 3. Test PHP
`> php -v`

#### 4. Install PHP extensions
`> sudo apt install php7.2-bcmath php7.2-bz2 php7.2-cgi php7.2-cli php7.2-common php7.2-curl php7.2-dev php7.2-enchant php7.2-fpm php7.2-gd php7.2-imap php7.2-intl php7.2-json php7.2-ldap php7.2-mbstring php7.2-odbc php7.2-opcache php7.2-pgsql php7.2-pspell php7.2-readline php7.2-sqlite3 php7.2-tidy php7.2-xml php7.2-xmlrpc php7.2-zip`

If you get this message, run the listed commands with sudo:
```
NOTICE: Not enabling PHP 7.2 FPM by default.
NOTICE: To enable PHP 7.2 FPM in Apache2 do:
NOTICE: a2enmod proxy_fcgi setenvif
NOTICE: a2enconf php7.2-fpm
NOTICE: You are seeing this message because you have apache2 package installed.
```

`> sudo service apache2 restart`

#### 5. SOAP (only if required)
`> sudo apt-get install php7.2-soap`

`> sudo service php7.2-fpm reload`

`> sudo service apache2 restart`

#### 6. Exit VM
`> exit`

---

## 5. Setup ModRewrite

#### 1. SSH into VM
`> vagrant ssh`

#### 2. Enabling mod_rewrite
`> sudo a2enmod rewrite`

`> sudo service apache2 restart`

#### 3. Setup .htaccess
`> sudo nano /etc/apache2/sites-available/000-default.conf`

Add this code to '000-default.conf' file, right after line: `<VirtualHost *:80>`
```
<Directory /var/www/html>
  Options Indexes FollowSymLinks MultiViews
  AllowOverride All
  Require all granted
</Directory>
```

`> sudo service apache2 restart`

`> sudo nano /var/www/html/.htaccess`

Add this code to .htaccess file:
```
RewriteEngine on
```

`> exit`

---

## 6. Link project folder

#### 1. Opend Vagrantfile

Create 'www' folder, in projct folder

Uncomment: `config.vm.synced_folder "LOCAL", "VIRTUAL"`

Change to: `config.vm.synced_folder "www/", "/var/www/html"`

`> vagrant reload`

---

## 7. Install MySQL

#### 1. SSH into VM
`> vagrant ssh`

#### 2. Install MySQL
`sudo apt-get install mysql-server php7.2-mysql`

When asked to set password: `root`

#### 3. Edit my.cnf
`sudo nano /etc/mysql/my.cnf`

Comment out:

`# skip-external-locking`

`# bind-address 0.0.0.0`

#### 4. Restart Apache and MySQL
`sudo service apache2 restart`

`sudo service mysql restart`

#### 5. Exit VM
`> exit`

---

## 8. Setup MySQL Workbench

#### 1. Create new connection
Hit the + icon to add a new connection

#### 2. Change connection method
Change dropbox to `Standard TCP/IP over SSH`

#### 3. Parameter settings

SSH Hostname: `192.168.33.10`

SSH Username: `vagrant`

SSH Key File: `c:\[project folder path]\.vagrant\machines\default\virtualbox\private_key`

MySQL Hostname: `127.0.0.1`

MySQL Server Port: `3306`

Username: `root`

#### 4. Start connection

SSH Password: `vagrant`

MySQL Password: `root`

---

## Composer

`> vagrant ssh`

`> curl -Ss https://getcomposer.org/installer | php`

`> sudo mv composer.phar /usr/bin/composer`
