# HTWG_VPN

* **Note:** In some systems the update-resolv-conf skript is already there, but doesn't work because ```resolvconf``` is missing.
* Store update-resolv-conf under ```/etc/openvpn/update-resolv-conf```, if you store the file anywhere else you have to update the path inside of the ovpn script.
* Make sure that the ```update-resolv-conf``` script is executable.
* Make sure ```resolvconf``` is installed (```sudo apt-get install resolvconf openresolv```), if you test it with the ```-h``` flag and it doesn't work correctly ```openresolv``` should be installed, too. This is a dependency that is sometimes missing, and that has to be installed manually. This issue can occur when you are working on an apt-based system.
* Now your HTWG-VPN should work and update the nameservers properly. This can be checked by executing ```cat /etc/resolv.conf``` before and after the login-procedure.

**EDIT:**
* There seems to be a problem with the openvpn installer-scripts. If you install openvpn with ```apt``` the ```update-resolv-conf``` script is set, but it tries to execute ```resolvconf``` which is not installed as dependencie. Additionaly ```openresolv``` seems not to be installed as ```resolvconf```-dependecy if you try to install it.
* With ```pacman``` the script seems to install all dependencies correcly but doesn't set the ```update-resolv-conf``` script so this should be set manually for example with the one in my respository.
* Our HTWG.ovpn script that you can get on our website the problem is that the security-level is set on 1 but to update the nameservers you need a level of 2.
