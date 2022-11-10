HTB(Meta-Linux)
===============

![](/Assets/HTB/Meta/pwned.png)

_**NMAP**_
-------------

![](/Assets/HTB/Meta/nmap.png)

_we found in scaning port 22 for ssh and port 80 for Apache._

_add ip in /etc/hosts and browse the http://artcorp.htb._

_ Go to take a look about website._

![](/Assets/HTB/Meta/browser.png)

_we will check subdomain by using *wfuzz*_

![](/Assets/HTB/Meta/fuzz.png) 

_we find subdomain *"dev01"* and we will add it in /etc/hosts._

![](/Assets/HTB/Meta/webhost.png) 

_the link **MetaView** take us to page to upload images_ 

![](/Assets/HTB/Meta/linkvhost.png) 

_after upload image to test and display their metadata._ 

![](/Assets/HTB/Meta/exictftool.png) 

_Further enumeration reveals the existence of a composer.json file._

![](/Assets/HTB/Meta/composer.png)

_we check the finds in enumration of **metaview** and use **curl** to show **EXIfTool** to read metadata._

![](/Assets/HTB/Meta/curl.png)

_**Foothold**_
---------------


_Searching for potential vulnerabilities we come across CVE-2021-22204, which could grant us remote
command execution in case of a vulnerable ExifTool version installed on the target. We use Git to clone the
repository of one of the available public exploits to our attacking machine._



![](/Assets/HTB/Meta/clone.png)

![](/Assets/HTB/Meta/cv.png)

_we will get in **expliot.py** and change ip to our ip which taken of htb vpn._ 

_after adding our ip will save and exit and run the expliot.py_ 

![](/Assets/HTB/Meta/run.png)

_will see two images will skip original and take second and upload it to web and before upload it open listening  on port which you specified as follow._

![](/Assets/HTB/Meta/shell.png)

_we see got shell._

_We upgrade our shell to a fully interactive pty:_ 

![](/Assets/HTB/Meta/upgrade.png)


_will use ** python3 -c 'import pty;pty.spawn("/bin/bash")'** in addition to ctrl+z_ 

_ in our console will tybe **stty raw -echo;fg** don not forget doble enter_ 



