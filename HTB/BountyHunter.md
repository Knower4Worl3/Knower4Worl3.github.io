
HTB(BountyHunter-Linux)
=======================


![](/Assets/HTB/BountyHunter/assets/BountyHunter.png)

_**Summary**_ 
-------------
_BountyHunter box has more info about things and we will use some tools like dirsearch and will know about source code reveiw and will xml injection to read php file and will use development user to foothold on system._


_**NMAP**_
----------

![](/Assets/HTB/BountyHunter/assets/nmap1.png)

_**PORTS**_
-----------
_We find port 22 fir ssh conection and Apache2 on port 80._ 

_we will take a tour in website we found a Bug Bounty Tracking System , the website have portal to submit your bug and **contact us** form that does not work correctly and **about**._

![](/Assets/HTB/BountyHunter/assets/web.png)


_will use **dirsearch** to take a look deeply on site._

![](/Assets/HTB/BountyHunter/assets/dirsearch.png)




![](/Assets/HTB/BountyHunter/assets/dirsearch1.png)



_we found file db.php its interesting file , we should go deep in resourses and with the same command in dirsearch to see deep in this folder._



![](/Assets/HTB/BountyHunter/assets/dirsearch2.png)



![](/Assets/HTB/BountyHunter/assets/dirsearch3.png)


_**Let's have a look at README.txt , which seems interesting.**_

_**curl http://10.129.95.166/resources/README.txt**_

![](/Assets/HTB/BountyHunter/assets/readme.png)


_now we find in **Readme.txt** development user is a test user that does not require password We return to the login
screen and attempt to get in using the username test and no password; this time it succeeds. We've landed
at the gateway page. Other than a single sentence referring us to another website, there is no more
valuable information. Let's go to portal and look around._


![](/Assets/HTB/BountyHunter/assets/portal.png)


_**Foothold**_
--------------
_after get in portal we will clicking on portal.php and will find the team's Bounty Tracking System._

![](/Assets/HTB/BountyHunter/assets/portal1.png)

_we can enter random data to see what is the reflect of form._ 

![](/Assets/HTB/BountyHunter/assets/pagedata.png)

_will use brupsuite tool to intercept the request to database of bugbounty system and we find as follow._ 

![](/Assets/HTB/BountyHunter/assets/burp1.png)


_the page sends request to **tracker_diRbPr00f314.php** , the payload was in html encoding and should to decode it and decode it again to base64 as follow._


![](/Assets/HTB/BountyHunter/assets/base64+.png)

![](/Assets/HTB/BountyHunter/assets/xmlcode.png)

_now we see the file after decoding is xml file , let's try read the file system by injecting XXE file._ 


![](/Assets/HTB/BountyHunter/assets/xxe.png)


_we will take this xml code in file.xml and encode it by base64 and add it in data= our encoded result as follow._ 

![](/Assets/HTB/BountyHunter/assets/coder.png)

_we url encoding and use Burp to send our request._ 

![](/Assets/HTB/BountyHunter/assets/response.png)

![](/Assets/HTB/BountyHunter/assets/r2.png)

_Now we'll be able to read any file we have access with this XXE injection. We can also try to read the db.php
file, and as this is an apache2 server, we are going to try by selecting */var/www/html/* path. First though we
need to base64 encode it using the php filter._


![](/Assets/HTB/BountyHunter/assets/xxe1.png)


_And now we can sent it._

![](/Assets/HTB/BountyHunter/assets/hash.png)

_now we have encoded result of request and we should decoded it as follow._

![](/Assets/HTB/BountyHunter/assets/password.png)

_It seems that we got some credentials and now it is possible to check if we can login. We are spraying this
password to system users we got from the /etc/passwd file and indeed we manage to get a successful
login with the user development ._

![](/Assets/HTB/BountyHunter/assets/ssh.png)

![](/Assets/HTB/BountyHunter/assets/user.png)

_now we done access on machine as user **development** and got flag user._

_**Privilege Escalation**_
===========================

_we check after get user flag we take a look about file contract we find valuble words and will search in /opt about what it has , will find skytrain_inc folder and have investgate tool to check tickets submitted ._

![](/Assets/HTB/BountyHunter/assets/contract.png)

_after check code ticketValidator.py we find function **eval** and how to spot on vulnerabilities._

![](/Assets/HTB/BountyHunter/assets/function.png)

_We also examine the ticket code to discover how it is calculated by the script._

![](/Assets/HTB/BountyHunter/assets/ticket.png)

_Also this is a supplementary check, to check the validator is more than value of 100._

![](/Assets/HTB/BountyHunter/assets/val.png)

_we see if create ticket and run it but this file work from root we will see if we can check sudoers if there is a way to excute it._

![](/Assets/HTB/BountyHunter/assets/sudo.png)

_will see we can use this commands by sudo as show in screen and will create ticket to see what will happen and make the result is true in file by extintion md._

![](/Assets/HTB/BountyHunter/assets/enumratecode3.png)

_by excute the command which allowable to sudo on development user with true ticket the validitor make validate the ticket make us root._ 

_This is a success. Now we can change id to /bin/bash and get an interactive root shell._

 ![](/Assets/HTB/BountyHunter/assets/root.png)
 
 ![](/Assets/HTB/BountyHunter/assets/rootflag.png)
 
 _Thanks For Watching My Blog_
 =============================
 
 _Mohamed Emam_
 
 
