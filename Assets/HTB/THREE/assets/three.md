# HTB(Three-Linux) 

![](/Assets/HTB/THREE/assets/three.jpg) 

# Summary 

* in this Box will new some steps in *cloud pentesting* and will know about *Amazon S3* and how we can know about its contents and how make our machine contact easily with it. 

# NMAP
![](/Assets/HTB/THREE/assets/nmap.png)

# Ports 
we find port 22 for ssh connection and port 80 for http service will discover it , let's check it by browser . 



![](/Assets/HTB/THREE/assets/web.png)



By checking the web using web by browser  we find the static page and will check the **subdomains** for this host by using **gobuster** as follow .

**NOTE** : add ip of machine in **/etc/hosts** 

![](/Assets/HTB/THREE/assets/gobuster.png)

we found subdomain will be foucs with it **s3.thetoppers.htb** by search on google about will find info about **amazon s3 cloud storage**

![](/Assets/HTB/THREE/assets/s3amazon.png)












