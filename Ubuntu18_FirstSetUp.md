# Ubuntu 18.04 Orientation

Install the below packages after you have install Ubunut 18.04
[Setting Up Ubuntu on VM ](https://dev.to/awwsmm/setting-up-an-ubuntu-vm-on-windows-server-2g23)

```sh
# update .bashrc with PS1
PS1='\[`[ $? = 0 ] && X=2 || X=1; tput setaf $X`\]\h\[`tput sgr0`\]:$PWD\n\$ '


sudo apt-get update && sudo apt-get upgrade -y
sudo apt-get install net-tools tree git openssh-server ifupdown ssh curl yum -y
sudo apt-get install make build-essential libssl-dev zlib1g-dev libbz2-dev \
    libreadline-dev libsqlite3-dev wget libncurses5-dev libncursesw5-dev \
    llvm xz-utils tk-dev libffi-dev liblzma-dev -y
sudo apt-get install gcc make -y
sudo apt-get install build-essential dkms linux-headers-$(uname -r) -y
sudo echo "$USERNAME ALL=NOPASSWD: ALL: >> /etc/sudoers
```
The best way to install Vim on Unix is to use the sources. This requires a compiler and its support files. Compiling Vim isn't difficult at all. You can simply type "make install" when you are happy with the default features. Edit the Makefile in the "src" directory to select specific features.
You need to download at the sources and the runtime files. And apply all the latest patches. For Vim 6 up to 7.2 you can optionally get the "lang" archive, which adds translated messages and menus. For 7.3 and later this is included with the runtime files.

Using git is the simplest and most efficient way to obtain the latest version, including all patches. This requires the "git" command.
The explanations are on the GitHub page.

```sh
git clone https://github.com/vim/vim.git
cd vim/src
make

```


## How to Install VirtualBox Guest Additions in Ubuntu
VirtualBox Guest Additions are a collection of device drivers and system applications designed to achieve closer integration between the host and guest operating systems. They help to enhance the overall interactive performance and usability of guest systems.
The VirtualBox Guest Additions offer the following features:
+ Easy mouse pointer integration.
+ Easy way to share folders between the host and the guest.
+ Drag and drop feature allows copying or opening files, copy clipboard formats from the host to the guest or from the guest to the host.
+ Share clipboard (for copy and paste) of the guest operating system with your host operating system.
+ Better video support provides accelerated video performance.
+ Better Time synchronization between guest and host.
+ Standard host/guest communication channels.
+ Seamless Windows features allows you to run windows of your guest operating system seamlessly next to the windows of your host.

The VirtualBox Guest Additions should be installed inside a virtual machine after the guest operating system has been installed.

### How to Install VirtualBox Guest Additions in Ubuntu
1. First start by updating your Ubuntu guest operating system software packages using following command.
```
$ sudo apt update
$ sudo apt upgrade
```
2. Once upgrade completes, reboot your Ubuntu guest operating system to effect the recent upgrades and install required packages as follows.
```
$ sudo apt install build-essential dkms linux-headers-$(uname -r)
```
3. Next, from the Virtual Machine menu bar, go to Devices => click on Insert Guest Additions CD image as shown in the screenshot. This helps to mount the Guest Additions ISO file inside your virtual machine.

4. Next, you will get a dialog window, prompting you to Run the installer to launch it.

5. A terminal window will be opened from which the actual installation of VirtualBox Guest Additions will be performed. Once the installation is complete, press [Enter] to close the installer terminal window. Then power off your Ubuntu guest OS to change some settings from VirtualBox manager as explained in the next step.

6. Now to enable Shared Clipboard and Drag’n’Drop functionality between Guest and Host Machine. Go to General => Advanced and enable the two options (Shared Clipboard and Drag’n’Drop) as you wish, from the drop down options. Then click OK to save the settings and boot your system, login and test if everything is working fine.

You have successfully installed VirtualBox Guest Additions on Ubuntu and Debian based distributions

### How to setup No Password for sudo
Update /etc/sudoers in the last line as
```
myusername ALL=NOPASSWD: ALL
```

### How to install vim 
1) Save the .vimrc file from this location to your home
2) search vundle for vim on google and clone the [git repo](https://github.com/VundleVim/Vundle.vim.git)
3) install vim & gvim ``` sudo yum install vim ```
4) Read [how-to-use-vundle-to-manage-vim-plugins-](https://www.digitalocean.com/community/tutorials/how-to-use-vundle-to-manage-vim-plugins-on-a-linux-vps)
5) Add Plugins for C++ [setting-up-vim-for-c-development](https://idorobotics.com/2018/04/01/setting-up-vim-for-c-development/)
6) Actual Vim.[tutorial-make-vim-as-your-cc-ide-using-cvim](https://www.thegeekstuff.com/2009/01/tutorial-make-vim-as-your-cc-ide-using-cvim-plugin/)


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
