# ubuntu 18 - set static IP

- [How to Configure Static IP address  on Ubuntu 18.04](https://linuxize.com/post/how-to-configure-static-ip-address-on-ubuntu-18-04/)

Create sudo nano /etc/netplan/01-netcfg.yaml and paste below

```bash
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
