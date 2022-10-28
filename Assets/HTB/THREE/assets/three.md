# HTB(Three-Linux) 

![](/Assets/HTB/THREE/assets/three.jpg) 

# Summary 

* in this Box will new some steps in *cloud pentesting* and will know about *Amazon S3* and how we can know about its contents and how make our machine contact easily with it. 

# NMAP
![](/Assets/HTB/THREE/assets/nmap.png)

# Ports 
we find port 22 for ssh connection and port 80 for http service will discover it , let's check it by browser . 



![](/Assets/HTB/THREE/assets/web.png)



By checking the web using web browser we find the static page and will check the **subdomains** for this host by using **gobuster** as follow .

**NOTE** : add ip of machine in **/etc/hosts** 

like that  echo **"10.129.10.31 thetoppers.htb" | sudo tee -a /etc/hosts**

![](/Assets/HTB/THREE/assets/gobuster.png)

we found subdomain will be foucs with it **s3.thetoppers.htb** by search on google about it , will find info about **amazon s3 cloud storage**

![](/Assets/HTB/THREE/assets/s3amazon.png)

_**NOTE**_  we should add the subdomain **s3.thetopper.htb** in /etc/hosts like that 

echo **"10.129.10.31 s3.thetoppers.htb" | sudo tee -a /etc/hosts** and will open the s3.thetoppers.htb in our browser will find that result . 

![](/Assets/HTB/THREE/assets/response.png)




















