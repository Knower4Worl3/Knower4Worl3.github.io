HTB(Meta-Linux)
===============

![](/Assets/HTB/Meta/reired.png)

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


_will use ** python3 -c 'import pty;pty.spawn("/bin/bash")'** in addition to ctrl+z._ 

_in our console will tybe **stty raw -echo;fg** do not forget double enter._ 

_We have successfully upgraded the shell. User flag is not accessible to user www-data. It is only readable to users root and thomas. After some enumeration when did not find anything interesting then ran $ pspy [a process monitoring tool] to check whether any file is being executed at regular interval. You can download pspy64 binary_ 

![](/Assets/HTB/Meta/pspy.png)

![](/Assets/HTB/Meta/runing.png)

![](/Assets/HTB/Meta/mog.png)

_pspy64s found convert_images.sh present at location /usr/local/bin/ is being executed at regular interval of 1 min by user thomas [check UID=1000, in above pspy report]. Let us check the content of this file._

![](/Assets/HTB/Meta/mography.png)

![](/Assets/HTB/Meta/ver.png)

_On checking the content of convert_images.sh found that it is executing $ mogrify command to convert each uploaded file to png. Check more about $ mogrify command , On checking the version of $ mogrify found that the version of **ImageMagick** suite of which it is part of is 7.0.10-36. After some googling found that ImageMagick 7.0.10-36 is vulnerable to Shell Injection vulnerability. Since $ mogrify is part of ImageMagick suite so it may also be vulnerable._

_To exploit this vulnerability, I have simply created a file poc.svg inside the directory /var/www/dev01.artcorp.htb/convert_images/ with the payload_

_We can exploit this to obtain a reverse shell as thomas . First we encode our reverse shell
payload to base64:_

_Then we create a file called rce.svg where our injected command will echo the base64 string generated
above, decode it and pass it to bash via a pipe. This will result in our payload being executed on the next
cron execution._

![](/Assets/HTB/Meta/echo.png)

![](/Assets/HTB/Meta/user.png)

![](/Assets/HTB/Meta/userflag1.png)

_Don't forget after take id_rsa on our machine to give it permission to work as follow **chmod 600 id_rsa**._

_we have access by ssh after take id_rsa from server to our machine._ 

_**Privlege Esclastion**_ 
--------------------------

_To esclate the privilege to root we should first the **privilege esclation vector** we can find privEsc either manullay or using scripts like linpeas.sh._ 

_**Finding PrivEsc Vector**_

![](/Assets/HTB/Meta/linsh.png)

![](/Assets/HTB/Meta/privilageEs.png)

_now we see that thomas user can run **/usr/bin/neofetch** but to run this neofetch binary requires a config file and that file is present in users home directory, for example if user thomas executes that will require confige file inside /home/thomas/ directory , if user root excute this file will require file in /root/ directory._

_lets's looking into **sudo -l** and we found environment varible XDG_CONFIG_HOME by search about that._ 


![](/Assets/HTB/Meta/XDC_CONFIG_HOME_env-variable-info.png)

_ based above explanantion 


