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


### When starting Virtual Box VM got the below Error everytime
/~/software/ParticleRuntime/v84/bin/glnxa64/libcurl.so.4: no version information available (required by curl)

__Solution-Working__

1. First locate the location of libcurl:
```sh
locate libcurl.so.4
Probably like this

 /usr/lib/x86_64-linux-gnu/libcurl.so.4
 /usr/lib/x86_64-linux-gnu/libcurl.so.4.3.0
 /usr/local/lib/libcurl.so.4
 /usr/local/lib/libcurl.so.4.4.0
```
2. Deleted the soft link for this conflict
```sh
 rm -rf /usr/local/lib/libcurl.so.4
```
3.Then, link the 4.3.0 static library to the top
```sh
ln -s /usr/lib/x86_64-linux-gnu/libcurl.so.4.3.0 /usr/local/lib/libcurl.so.4
```


```sh
<deeps@sdcndub:/usr/local/lib
>sudo rm -rf libcurl.so.4
<deeps@sdcndub:/usr/local/lib
>ls -alrt libcurl*       
-rwxr-xr-x 1 root root 1857168 Sep 30  2018 libcurl.so.4.0.0
lrwxrwxrwx 1 root root      16 Sep 30  2018 libcurl.so -> libcurl.so.4.0.0
-rwxr-xr-x 1 root root     889 Sep 30  2018 libcurl.la
-rw-r--r-- 1 root root 4442650 Sep 30  2018 libcurl.a
<deeps@sdcndub:/usr/local/lib
>sudo ln -s /usr/lib/x86_64-linux-gnu/libcurl.so.4.5.0 /usr/local/lib/libcurl.so.4
<deeps@sdcndub:/usr/local/lib
>ls -alrt
total 6184
drwxrwsr-x  3 root staff    4096 Sep 29  2018 python3.6
-rwxr-xr-x  1 root root  1857168 Sep 30  2018 libcurl.so.4.0.0
lrwxrwxrwx  1 root root       16 Sep 30  2018 libcurl.so -> libcurl.so.4.0.0
-rwxr-xr-x  1 root root      889 Sep 30  2018 libcurl.la
-rw-r--r--  1 root root  4442650 Sep 30  2018 libcurl.a
drwxr-xr-x  2 root root     4096 Sep 30  2018 pkgconfig
drwxr-xr-x 11 root root     4096 Jun 13  2019 ..
drwxrwsr-x  4 root staff    4096 Jan  1 10:47 python2.7
drwxr-xr-x  6 root root     4096 Jan 21 22:09 node_modules
lrwxrwxrwx  1 root root       42 Feb 19 21:49 libcurl.so.4 -> /usr/lib/x86_64-linux-gnu/libcurl.so.4.5.0
drwxr-xr-x  6 root root     4096 Feb 19 21:49 .
<deeps@sdcndub:/usr/local/lib
>ls -alrt libcurl.so.4
lrwxrwxrwx 1 root root 42 Feb 19 21:49 libcurl.so.4 -> /usr/lib/x86_64-linux-gnu/libcurl.so.4.5.0
<deeps@sdcndub:/usr/local/lib

```


