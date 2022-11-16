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

_Now we have **hazard** and **rout3r** as **usernames** and **Stealth1agent, $uperP@ssword, Q4)sJu\Y8qz*A3?d** as passwords._ 

_will try authenticate to smb as **hazard:stealth1agent**._ will use **Iookupsid.py** from **Impacket** to enumerate the other users._ 

![](/Assets/HTB/Heist/enumrateuers.png)

_we find user **Chase** will authenticate to winrm as **chase:Q4)sJu\Y8qz*A3?d**._ 

![](/Assets/HTB/Heist/user.png)

![](/Assets/HTB/Heist/userflag.png)


_will use firefox process dump to get administrator password._ 
--------------------------------------------------------------



_will get in **\appdata\Romaing\Mozilla** and take a look about what it have._

![](/Assets/HTB/Heist/mozillaa.png)


_And there some firefox proxesses runing._

![](/Assets/HTB/Heist/mozillac.png)

_We uploaded procdump.exe and dumped one of these processes._

_and will get in **cd C:\Windows\System32\spool\drivers\color** and upload **procdump64.exe**._

_we here choose process **6972** to dump it._

![](/Assets/HTB/Heist/procdumb.png)


_Then I uploaded strings.exe and used it on the dump and saved the output to another file._

![](/Assets/HTB/Heist/strings.png)

_we search about word "password" and found administrator password in exposed requests._

![](/Assets/HTB/Heist/findstr.png)

_we can use **psexec.py** to get root._ 

![](/Assets/HTB/Heist/root.png)

![](/Assets/HTB/Heist/rootflag.png)

_**Thanks for watching my Blog**_
----------------------------------

_Mohamed Emam_
---------------






































