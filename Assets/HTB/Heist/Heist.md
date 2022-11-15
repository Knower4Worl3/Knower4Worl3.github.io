_**HTB(Heist-Windows)**_
==========================


![](/Assets/HTB/Heist/cong.png)


_**NMAP**_
----------

_let's strart enumrate about open ports and services._

![](/Assets/HTB/Heist/nmap.png)

_we found port 80 and smb , in addition to will run another scan about winrm on port 5985._ 

![](/Assets/HTB/Heist/winrm.png) 

_we found port winrm is opened._

![](/Assets/HTB/Heist/smbsail.png)

_we try to get in smb by anonymouse user but not authinticated._

_**Web Enumration**_
--------------------

_let's check web._

![](/Assets/HTB/Heist/web.png)

_we found login user form._

_we will try to open as guest._ 

![](/Assets/HTB/Heist/openguset.png)

_there was user called **hazard** post about part of configurations of router cisco with some hashed credentials._

![](/Assets/HTB/Heist/attachment.png)

_By using online tool to cracking the passwords._ 

![](/Assets/HTB/Heist/cracka.png)

![](/Assets/HTB/Heist/crackb.png)

And for the other hash I cracked it with john:

![](/Assets/HTB/Heist/hash.png)







