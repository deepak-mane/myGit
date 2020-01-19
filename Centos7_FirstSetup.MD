# Centos7 - First Setup - Installing MySQL Database


### How to Install mysql on centos7
CentOS 7 prefers MariaDB, a fork of MySQL managed by the original MySQL developers and designed as a replacement for MySQL. If you run yum install mysql on CentOS 7, it is MariaDB that is installed rather than MySQL. If you’re wondering about MySQL vs. MariaDB, MariaDB will generally work seamlessly in place of MySQL, so unless you have a specific use-case for MySQL, see the How To Install MariaDB on Centos 7 guide.

- <b>Step 1 — Installing MySQL</b>
1. From https://dev.mysql.com/downloads/repo/yum/ find correct version of rpm needed for your OS (mysql80-community-release-el7-3.noarch.rpm)
2. Run command ``` wget https://dev.mysql.com/get/mysql80-community-release-el7-3.noarch.rpm ```
3. Verify the integrity of the download by running md5sum and comparing it with the corresponding MD5 value listed on the site
  
```ssh
export myvar=$(md5sum mysql80-community-release-el7-3.noarch.rpm | awk '{print $1}')
if [ $myvar == "893b55d5d885df5c4d4cf7c4f2f6c153" ];then  
    echo "PASS" ; 
else 
    echo "FAIL" ;
fi
```
  4. This adds two new MySQL yum repositories, and we can now use them to install MySQL server:

```ssh 
sudo rpm -ivh mysql80-community-release-el7-3.noarch.rpm
```
  5. ```ssh sudo yum install mysql-server ```
sudo yum install mysql-server
Press y to confirm that you want to proceed. Since we’ve just added the package, we’ll also be prompted to accept its GPG key. Press y to download it and complete the install.

Install MySQL workbench which would be needed for GUI interface when working on Linux systems
```
sudo yum install mysql-workbench-community

# To Launch the MySQL Workbench from terminal run below command:
mysql-workbench

# This should popup GUI window where you enter the root password for the first time 
# save in the keychain ring by entering the hosts login credentials for authentication purposes.
```

- <b>Step 2 — Starting MySQL</b>
  1. We’ll start the daemon with the following command: 
  
  ``` sudo systemctl start mysqld ```
  
  systemctl doesn’t display the outcome of all service management commands, so to be sure we succeeded, we’ll use the following command: 
  
  ``` sudo systemctl status mysqld ```
  
  If MySQL has successfully started, the output should contain Active: active (running) and the final line should look something like:

    ```
    Dec 01 19:02:20 centos-512mb-sfo2-02 systemd[1]: Started MySQL Server.
    ```

Note: MySQL is automatically enabled to start at boot when it is installed. You can change that default behavior with sudo systemctl disable mysqld

During the installation process, a temporary password is generated for the MySQL root user. Locate it in the mysqld.log with this command:

    ```
    sudo grep 'temporary password' /var/log/mysqld.log
    Output
    2016-12-01T00:22:31.416107Z 1 [Note] A temporary password is generated for 
    root@localhost: mqRfBU_3Xk>r
    ```

Make note of the password, which you will need in the next step to secure the installation and where you will be forced to change it. The default password policy requires 12 characters, with at least one uppercase letter, one lowercase letter, one number and one special character.

- <b>Step 3 — Configuring MySQL</b>
MySQL includes a security script to change some of the less secure default options for things like remote root logins and sample users.

Use this command to run the security script. 

``` sudo mysql_secure_installation ```

This will prompt you for the default root password. As soon as you enter it, you will be required to change it.

    ```
    Output
    The existing password for the user account root has expired. 
    Please set a new password.
    New password:
    ```

Enter a new 12-character password that contains at least one uppercase letter, one lowercase letter, one number and one special character. Re-enter it when prompted.

You’ll receive feedback on the strength of your new password, and then you’ll be immediately prompted to change it again. Since you just did, you can confidently say No:

    ```
    Output
    Estimated strength of the password: 100
    Change the password for root ? (Press y|Y for Yes, any other key for No) :
    After we decline the prompt to change the password again, we’ll press Y
    and then ENTER to all the subsequent questions in order to remove 
    anonymous users, disallow remote root login, remove the test database 
    and access to it, and reload the privilege tables.
    ```

Now that we’ve secured the installation, let’s test it.

- <b>Step 4 — Testing MySQL</b>
We can verify our installation and get information about it by connecting with the mysqladmin tool, a client that lets you run administrative commands. Use the following command to connect to MySQL as root (-u root), prompt for a password (-p), and return the version.

    ```
    mysqladmin -u root -p version
    ```

You should see output similar to this:

    ```
    Output
    mysqladmin  Ver 8.42 Distrib 5.7.16, for Linux on x86_64
    Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

    Oracle is a registered trademark of Oracle Corporation and/or its
    affiliates. Other names may be trademarks of their respective
    owners.

    Server version          5.7.16
    Protocol version        10
    Connection              Localhost via UNIX socket
    UNIX socket             /var/lib/mysql/mysql.sock
    Uptime:                 2 min 17 sec

    Threads: 1  Questions: 6  Slow queries: 0  Opens: 107  Flush tables: 1  
    Open tables: 100  Queries per second avg: 0.043
    ```
This indicates your installation has been successful.

- <b>Conclusion</b>
In this tutorial, we’ve installed and secured MySQL on a CentOS 7 server. To learn more about using MySQL, this guide to learning more about MySQL commands can help. You might also consider implementing some additional security measures.

```ssh
$ sudo yum install mysql-server
[sudo] password for sysadmin: 
Loaded plugins: fastestmirror, langpacks
Loading mirror speeds from cached hostfile
 * base: mirrors.cat.pdx.edu
 * extras: mirrors.cat.pdx.edu
 * updates: mirrors.cat.pdx.edu
mysql-connectors-community                                  | 2.5 kB  00:00:00     
mysql-tools-community                                       | 2.5 kB  00:00:00     
mysql80-community                                           | 2.5 kB  00:00:00     
(1/3): mysql-connectors-community/x86_64/primary_db         |  53 kB  00:00:00     
(2/3): mysql-tools-community/x86_64/primary_db              |  69 kB  00:00:00     
(3/3): mysql80-community/x86_64/primary_db                  |  97 kB  00:00:00     
Resolving Dependencies
--> Running transaction check
---> Package mysql-community-server.x86_64 0:8.0.19-1.el7 will be installed
--> Processing Dependency: mysql-community-common(x86-64) = 8.0.19-1.el7 for package: mysql-community-server-8.0.19-1.el7.x86_64
--> Processing Dependency: mysql-community-client(x86-64) >= 8.0.11 for package: mysql-community-server-8.0.19-1.el7.x86_64
--> Running transaction check
---> Package mysql-community-client.x86_64 0:8.0.19-1.el7 will be installed
--> Processing Dependency: mysql-community-libs(x86-64) >= 8.0.11 for package: mysql-community-client-8.0.19-1.el7.x86_64
---> Package mysql-community-common.x86_64 0:8.0.19-1.el7 will be installed
--> Running transaction check
---> Package mariadb-libs.x86_64 1:5.5.60-1.el7_5 will be obsoleted
--> Processing Dependency: libmysqlclient.so.18()(64bit) for package: 2:postfix-2.10.1-7.el7.x86_64
--> Processing Dependency: libmysqlclient.so.18(libmysqlclient_18)(64bit) for package: 2:postfix-2.10.1-7.el7.x86_64
---> Package mysql-community-libs.x86_64 0:8.0.19-1.el7 will be obsoleting
--> Running transaction check
---> Package mysql-community-libs-compat.x86_64 0:8.0.19-1.el7 will be obsoleting
--> Finished Dependency Resolution

Dependencies Resolved

===================================================================================
 Package                       Arch     Version          Repository           Size
===================================================================================
Installing:
 mysql-community-libs          x86_64   8.0.19-1.el7     mysql80-community   4.0 M
     replacing  mariadb-libs.x86_64 1:5.5.60-1.el7_5
 mysql-community-libs-compat   x86_64   8.0.19-1.el7     mysql80-community   1.3 M
     replacing  mariadb-libs.x86_64 1:5.5.60-1.el7_5
 mysql-community-server        x86_64   8.0.19-1.el7     mysql80-community   436 M
Installing for dependencies:
 mysql-community-client        x86_64   8.0.19-1.el7     mysql80-community    41 M
 mysql-community-common        x86_64   8.0.19-1.el7     mysql80-community   605 k

Transaction Summary
===================================================================================
Install  3 Packages (+2 Dependent packages)

Total download size: 483 M
Is this ok [y/d/N]: y
Downloading packages:
warning: /var/cache/yum/x86_64/7/mysql80-community/packages/mysql-community-common-8.0.19-1.el7.x86_64.rpm: Header V3 DSA/SHA1 Signature, key ID 5072e1f5: NOKEY
Public key for mysql-community-common-8.0.19-1.el7.x86_64.rpm is not installed
(1/5): mysql-community-common-8.0.19-1.el7.x86_64.rpm       | 605 kB  00:00:00     
(2/5): mysql-community-libs-8.0.19-1.el7.x86_64.rpm         | 4.0 MB  00:00:01     
(3/5): mysql-community-libs-compat-8.0.19-1.el7.x86_64.rpm  | 1.3 MB  00:00:00     
(4/5): mysql-community-client-8.0.19-1.el7.x86_64.rpm       |  41 MB  00:00:05     
(5/5): mysql-community-server-8.0.19-1.el7.x86_64.rpm       | 436 MB  00:00:43     
-----------------------------------------------------------------------------------
Total                                                  10 MB/s | 483 MB  00:46     
Retrieving key from file:///etc/pki/rpm-gpg/RPM-GPG-KEY-mysql
Importing GPG key 0x5072E1F5:
 Userid     : "MySQL Release Engineering <mysql-build@oss.oracle.com>"
 Fingerprint: a4a9 4068 76fc bd3c 4567 70c8 8c71 8d3b 5072 e1f5
 Package    : mysql80-community-release-el7-3.noarch (installed)
 From       : /etc/pki/rpm-gpg/RPM-GPG-KEY-mysql
Is this ok [y/N]: y
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
Warning: RPMDB altered outside of yum.
  Installing : mysql-community-common-8.0.19-1.el7.x86_64                      1/6 
  Installing : mysql-community-libs-8.0.19-1.el7.x86_64                        2/6 
  Installing : mysql-community-client-8.0.19-1.el7.x86_64                      3/6 
  Installing : mysql-community-server-8.0.19-1.el7.x86_64                      4/6 
  Installing : mysql-community-libs-compat-8.0.19-1.el7.x86_64                 5/6 
  Erasing    : 1:mariadb-libs-5.5.60-1.el7_5.x86_64                            6/6 
  Verifying  : mysql-community-libs-8.0.19-1.el7.x86_64                        1/6 
  Verifying  : mysql-community-libs-compat-8.0.19-1.el7.x86_64                 2/6 
  Verifying  : mysql-community-client-8.0.19-1.el7.x86_64                      3/6 
  Verifying  : mysql-community-common-8.0.19-1.el7.x86_64                      4/6 
  Verifying  : mysql-community-server-8.0.19-1.el7.x86_64                      5/6 
  Verifying  : 1:mariadb-libs-5.5.60-1.el7_5.x86_64                            6/6 

Installed:
  mysql-community-libs.x86_64 0:8.0.19-1.el7                                       
  mysql-community-libs-compat.x86_64 0:8.0.19-1.el7                                
  mysql-community-server.x86_64 0:8.0.19-1.el7                                     

Dependency Installed:
  mysql-community-client.x86_64 0:8.0.19-1.el7                                     
  mysql-community-common.x86_64 0:8.0.19-1.el7                                     

Replaced:
  mariadb-libs.x86_64 1:5.5.60-1.el7_5                                             

Complete!
(base) centos7:/tmp
$ 


````

### Creating User and setup

```
# check version after installation
mysqladmin -u root -p version 
# Create User
CREATE USER 'username'@'localhost' IDENTIFIED BY '12charpassword';
## GRANT ALL PRIVILEGES ON database.table TO 'deecent'@'localhost';
grant all privileges on *.* to 'deecent'@'localhost';
# In order for the changes to take effect and the privileges to be 
# saved the following command should be executed at the end:
FLUSH PRIVILEGES;
mysql -p -u deecent
```

### Important Setup After Above mysql installation and changing default root password
1) Install mysql workbench ``` sudo yum install mysql-workbench-community ```
2) Create a database in mysql database server 

```
mysql> create database `blog_data`
    -> ;
Query OK, 1 row affected (0.01 sec)

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| blog_data          |
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
5 rows in set (0.01 sec)

mysql> quit
Bye

```
3) Install mysqlclient using pip

```
You should install the mysql first:
yum install python-devel mysql-community-devel -y
Then you can install mysqlclient:
pip install  mysqlclient

$ pip install  mysqlclient
Collecting mysqlclient
  Using cached https://files.pythonhosted.org/packages/../../mysqlclient-1.4.6.tar.gz
Installing collected packages: mysqlclient
    Running setup.py install for mysqlclient ... done
Successfully installed mysqlclient-1.4.6
(virtual) (base) centos7:/opt/dental/dental
```
4) In settings.py update ``` ALLOWED_HOSTS = ["192.168.1.XX"] ```

