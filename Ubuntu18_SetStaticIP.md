# ubuntu 18 - set static IP

- [How to Configure Static IP address  on Ubuntu 18.04](https://linuxize.com/post/how-to-configure-static-ip-address-on-ubuntu-18-04/)

Create sudo nano /etc/netplan/01-netcfg.yaml and paste below

```sh
network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s8:
      dhcp4: no
      addresses:
        - 192.168.1.30/24
      gateway4: 192.168.1.1
      nameservers:
          addresses: [8.8.8.8, 1.1.1.1]

```
Contents of netplan directory
```sh
deeps@ubuntu-ipc:/etc/netplan$ ls -alrt
total 24
-rw-r--r--   1 root root   104 Aug  5 12:11 01-network-manager-all.yaml
drwxr-xr-x 125 root root 12288 Jan  1 13:26 ..
-rw-r--r--   1 root root   214 Jan  1 13:40 01-netcfg.yaml
drwxr-xr-x   2 root root  4096 Jan  1 13:40 .
deeps@ubuntu-ipc:/etc/netplan$

```
