
HTB(BountyHunter-Linux)

![](/Assets/HTB/BountyHunter/assets/BountyHunter.png)

_**Summary**_ 

_BountyHunter box has more info about things and we will use some tools like dirsearch and will know about source code reveiw and will xml injection to read php file and will use development user to foothold on system_


_**NMAP**_

![](/Assets/HTB/BountyHunter/assets/nmap1.png)

_**PORTS**_

_We find port 22 fir ssh conection and Apache2 on port 80_ 

_we will take a tour in website we found a Bug Bounty Tracking System , the website have portal to submit your bug and **contact us** form that does not work correctly and **about**._

![](/Assets/HTB/BountyHunter/assets/web.png)


_will use **dirsearch** to take a look deeply on site._

![](/Assets/HTB/BountyHunter/assets/dirsearch.png)


![](/Assets/HTB/BountyHunter/assets/dirsearch1.png)

_we found file db.php its interesting file , we should go deep in resourses and with the same command in dirsearch to see deep in this folder._

![](![](/Assets/HTB/BountyHunter/assets/dirsearch2.png)

![](![](/Assets/HTB/BountyHunter/assets/dirsearch3.png)










