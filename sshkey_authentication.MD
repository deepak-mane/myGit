# SSH Keys and Authentication

- Download PuTTy and unzip.
  + generate private and public keys on laptop
  + save them as mykey.pub and mykey.ppk respectively
  + Don't enter passphrase while creating keys
  + Set ssh2 1048 when creating keys
  + Copy mykey.pub to target server
  + Run command: 
```
ssh-keygen -if mykey.pub > ssh2_mykeypub
cat ssh2_mykeypub >> ~/.ssh/authorized_keys
```

- Create shortcut under Start programs to start pageant.exe at boot time
```
C:\Users\%USERNAME%\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup
Create Shortcut name PAGEANT.EXE
Target: C:\D\APP\putty\PAGEANT.EXE "C:\D\APP\putty\mykey.ppk"
Start in: C:\D\APP\putty
```
### With this the private key mykey.ppk will always load in pageant service and be forward when using authenctication

Go to cmd prompt
Type
```
putty remote_user@remote_host
```
This should log you without password



# Using .pem key ssh to remote host

First cache the key
```cmd
echo y | plink -ssh username@host "exit"
```

On Linux Do
```
sudo yum install putty
```

Using Puttygen , load priavte key , Navigate to Conversions, Selecte Export Open sshkey and save with name mykey.pem

To convert permissions on Windows
```
click right on mykey.per file
security > options advanced > disable heritage
add > select entity o group > "type your user windows" > confirm name > accept > set basic perm > accept
```
To Logon to server using .pem key now type below:
```
ssh -i mykey.pem user@mydomain.com
```
# Why am I still getting a password prompt with ssh with public key authentication?
Make sure the permissions on the ~/.ssh directory and its contents are proper. When I first set up my ssh key auth, I didn't have the ~/.ssh folder properly set up, and it yelled at me.

Your home directory ~, your ~/.ssh directory and the ~/.ssh/authorized_keys file on the remote machine must be writable only by you: rwx------ and rwxr-xr-x are fine, but rwxrwx--- is no good¹, even if you are the only user in your group (if you prefer numeric modes: 700 or 755, not 775).
If ~/.ssh or authorized_keys is a symbolic link, the canonical path (with symbolic links expanded) is checked.
Your ~/.ssh/authorized_keys file (on the remote machine) must be readable (at least 400), but you'll need it to be also writable (600) if you will add any more keys to it.
Your private key file (on the local machine) must be readable and writable only by you: rw-------, i.e. 600.
Also, if SELinux is set to enforcing, you may need to run restorecon -R -v ~/.ssh (see e.g. Ubuntu bug 965663 and Debian bug report #658675; this is patched in CentOS 6).

```sh
# 
(base) centos7:/home/sysadmin/.ssh
$ ls -lart
total 20
-rw-rw-r--.  1 sysadmin sysadmin  387 Feb  2 10:19 authorized_keys
-rw-r--r--.  1 sysadmin sysadmin  406 Feb  3 23:24 id_rsa.pub
-rw-------.  1 sysadmin sysadmin 1679 Feb  3 23:24 id_rsa
drwx------.  2 sysadmin sysadmin   80 Feb  3 23:40 .
-rw-r--r--.  1 sysadmin sysadmin  803 Feb  3 23:46 known_hosts
drwx------. 33 sysadmin sysadmin 4096 Feb 10 22:51 ..
(base) centos7:/home/sysadmin/.ssh
$ chmod 600 authorized_keys
(base) centos7:/home/sysadmin/.ssh
$ ls -alrt
total 20
-rw-------.  1 sysadmin sysadmin  387 Feb  2 10:19 authorized_keys
```
