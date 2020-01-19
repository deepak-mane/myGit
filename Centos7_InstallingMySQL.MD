# Centos7 - First Setup - Installing MySQL Database



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
