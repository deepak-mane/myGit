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
