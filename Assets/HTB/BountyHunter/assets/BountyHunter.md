
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









