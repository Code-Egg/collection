# OpenLiteSpeed WordPress Collection for Ansible
[![Build Status](https://travis-ci.com/Code-Egg/ansible-lomp-wp.svg?branch=master)](https://github.com/Code-Egg/ansible-lomp-wp)

This collection contains:
  - [WordPress](https://wordpress.org/)
  - [OpenLiteSpeed](https://openlitespeed.org/)
  - [MySQL](https://www.mysql.com/)
  - [PHP](https://www.litespeedtech.com/open-source/litespeed-sapi/php)

Supports on an Ubuntu system. A virtualhost will be created with the options specified in the vars/default.yml variable file.

## Usage
### 1. Environment
Install ansible on center server
```
apt update && apt install ansible -y
```
Add SSH key to the client/node server so center server can ssh to it without password

### 2. Install this collection
```
ansible-galaxy collection install code_egg.openlitespeed_wordpress
```

### 3. Customize Options
Update `example.com` from inventory to your client server's domain/IP
```
vim inventory
```

Update SQL password, Domain name ..etc, from vars/default.yml
```
vim vars/default.yml
```
```yml
---
# System Settings
owner: www-data
group: www-data

#PHP Settings
php_version: "74"
php_dversion: "7.4"
php_opt_modules: [ 'lsphp{{ php_version }}-curl', 'lsphp{{ php_version }}-imagick', 'lsphp{{ php_version }}-intl', 'lsphp{{ php_version }}-opcache', 'lsphp{{ php_version }}-memcached', 'lsphp{{ php_version }}-tidy' ]
php_memory_limit: "128"
php_max_execution_time: "60"
php_upload_max_filesize: "128M"
php_post_max_size: "128M"

#MySQL Settings
mysql_root_password: "mysql_root_password"
mysql_db: "wordpress"
mysql_user: "egguser"
mysql_password: "password"

#HTTP Settings
http_host: "your_domain"
http_port: "80"
https_port: "443"
doc_root: "/var/www/{{ http_host }}"
ssl_key: "/usr/local/lsws/admin/conf/webadmin.key"
ssl_crt: "/usr/local/lsws/admin/conf/webadmin.crt"
```

### 4. Run ansible playbook
```command
ansible-playbook playbook.yml
```
