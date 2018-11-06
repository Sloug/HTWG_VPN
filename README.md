# HTWG_VPN

* **Note:** In some systems the update-resolv-conf skript is already there, but doesn't work because ```resolvconf``` is missing.
* Store update-resolv-conf under ```/etc/openvpn/update-resolv-conf```, if you store the file anywhere else you have to update the path inside of the ovpn script.
* Make sure that the ```update-resolv-conf``` script is executable.
* Make sure ```resolvconf``` is installed (```sudo apt-get install resolvconf openresolv```), if you test it with the ```-h``` flag and it doesn't work correctly ```openresolv``` should be installed, too. This is a dependency that is sometimes missing, and that has to be installed manually. This issue can occur when you are working on an apt-based system.
* Now your HTWG-VPN should work and update the nameservers properly. This can be checked by executing ```cat /etc/resolv.conf``` before and after the login-procedure.

