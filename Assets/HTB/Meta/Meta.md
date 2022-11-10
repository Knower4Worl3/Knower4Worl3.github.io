HTB(Meta-Linux)
===============

![](/Assets/HTB/Meta/pwned.png)

_**NMAP**_
-----------

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


















