---
layout: post
title: "Using MySQL with Bitnami on Vagrant VM"
date: 2013-07-08 17:52
comments: true
categories: 
---

The [Bitnami install doccumented earlier][install] is a bit broken relative to MySQL.
Evidently, when Bitnami installs in the VM situation and moves itself to the `/opt/rubystack...` 
directory, it expects to be a slightly more traditional install and use the userid mysql for
running the MySQL server.  However, the built databases are secured to the vagrant user account
(at least in my release).  This is relatively easy to confirm, try starting the server

     sudo ~/rubystack/ctlscript.sh start mysql

and not that it fails (after a bit).  One can look at the `mysqld.log` in `~/rubystack/mysql/data`
directory and see access errors.

The fix is to give the mysql user access to the MySQL data directory:

    cd ~/rubystack/mysql  
    chown -R mysql.vagrant data

After this is done, the startup command should work.

## To start MySQL

    cd rubystack  
    sudo ./ctlscript.sh start mysql

## To stop MySQL

    cd rubystack  
    sudo ./ctlscript.sh stop mysql

## Create MySQL databases for dev, test, production ##

The following sequence setups the development, test, and production databases for the
Rails project *tbd4students*.  

    tbd4students> mysql -u root
    CREATE DATABASE tbd4students_development DEFAULT CHARACTER SET utf8;
    GRANT ALL PRIVILEGES ON tbd4students_development.* TO 'vagrant'@'localhost' IDENTIFIED BY 'password';
    CREATE DATABASE tbd4students_test DEFAULT CHARACTER SET utf8;
    GRANT ALL PRIVILEGES ON tbd4students_test.* TO 'vagrant'@'localhost' IDENTIFIED BY 'password';
    CREATE DATABASE tbd4students_production DEFAULT CHARACTER SET utf8;
    GRANT ALL PRIVILEGES ON tbd4students_production.* TO 'vagrant'@'localhost' IDENTIFIED BY 'password';
    EXIT;

In this example, the username `vagrant` (default in the VM) with a password of
'`password`' is used to access the server.  There is also a presumption that
the root password to the MySQL server is blank.  This configuration, of
course, is NO security and is only useful when on a closed system.  One should
research how to configure things more  securely for anything that will be
Internet (or even LAN) visible.


[install]: /blog/2013/06/06/using-bitnamis-rubystack-on-virtualbox-linux-with-vagrant/
