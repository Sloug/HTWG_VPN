# HTWG_VPN

Store update-resolv-conf under /etc/openvpn/update-resolv-conf, if you store the file anywhere else you have to update the path inside of the ovpn script.
Make sure that the update-resolv-conf script is executable.
Make sure resolvconf is installed, if you test it with the -h command and it doesn't work correctly openresolv should be installed, too. This is a dependency but it seems that apt is missing the installation of this tool sometimes, if you are working on an apt based system this issue can occur.
Now your HTWG-VPN should work properly and updates the nameservers. You can check that by executing cat /etc/resolv.conf before and after the login-procedure.
