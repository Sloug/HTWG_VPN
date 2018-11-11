# VPN-Konfiguration der HTWG Konstanz

This is an additional explanation to [this](https://www.htwg-konstanz.de/en/rz/dienste/vpn-verbindung/)
If you are using a Linux-System to access the VPN, you may run into some trouble. This Guide will help you to find your way through everything that is neccessary to successfully connect to the VPN.

First of all, it depends on the Distribution you are using. We have tested Arch- and Debian-based Systems (Ubuntu is based on Debian, just in case you dont know ;-)).

## General explanation:
First of all, you have to download the .ovpn-File from the [HTWG Webpage](https://www.htwg-konstanz.de/en/rz/dienste/vpn-verbindung/). If this is done, you have to run this File with openvpn. You have two possibillities to achieve this: either you choose the graphical Linux-native tools to add your OpenVPN-File (in the Network Connections settings), but we would recommend you to choose the terminal, because we will explain it that way.
Everything else you have to do, is to start the OVPN-Script. Launch a terminal and type ```openvpn <path to .ovpn-file>```. You will be prompted to enter your HTWG-Username and Password. Eveything should be working fine now. IF NOT: CONTINUE READING!
  
## The Problem:
Maybe you realized that you cannot access any internal HTWG-Service, or that Name Resolution in General is not working properly. (Name Resolution descibes the process of getting the IP-Address that is behind a Domain-Name like htwg-konstanz.de)
This Problem occours when the .ovpn-File is launched and tries to update the ```/etc/resolv.conf```. It is neccessary to do some changes to this file, because we need a new DNS-Server enty if we are using the HTWG-VPN and if we would like to connect to any HTWG-Service (like accessing your container to do your required tasks for BSYS or SYSO). In the next step, we will clearify how you can get the HTWG-DNS-Server running in your VPN-Environment.

## The Solution:




* **Note:** In some systems the update-resolv-conf skript is already there, but doesn't work because ```resolvconf``` is missing.
* Store update-resolv-conf under ```/etc/openvpn/update-resolv-conf```, if you store the file anywhere else you have to update the path inside of the ovpn script.
* Make sure that the ```update-resolv-conf``` script is executable.
* Make sure ```resolvconf``` is installed (```sudo apt-get install resolvconf openresolv```), if you test it with the ```-h``` flag and it doesn't work correctly ```openresolv``` should be installed, too. This is a dependency that is sometimes missing, and that has to be installed manually. This issue can occur when you are working on an apt-based system.
* Now your HTWG-VPN should work and update the nameservers properly. This can be checked by executing ```cat /etc/resolv.conf``` before and after the login-procedure.

**EDIT:**
* There seems to be a problem with the openvpn installer-scripts. If you install openvpn with ```apt``` the ```update-resolv-conf``` script is set, but it tries to execute ```resolvconf``` which is not installed as dependencie. Additionaly ```openresolv``` seems not to be installed as ```resolvconf```-dependecy if you try to install it.
* With ```pacman``` the script seems to install all dependencies correcly but doesn't set the ```update-resolv-conf``` script so this should be set manually for example with the one in my respository.
* Our HTWG.ovpn script that you can get on our website the problem is that the security-level is set on 1 but to update the nameservers you need a level of 2.
