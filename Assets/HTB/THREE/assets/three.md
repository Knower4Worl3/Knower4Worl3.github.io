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


![](/Assets/HTB/THREE/assets/response.png)

The webpage only contains the perivous JSON.

We can interact with this S3 bucket with the aid of the **awscli** utility. It can be installed on Linux using the command **apt install awscli** 

First, we need to configure it using the following command. **aws configure**

![](/Assets/HTB/THREE/assets/aws.png)

We can list all of the S3 buckets hosted by the server by using the ls command.

**aws --endpoint=http://s3.thetoppers.htb s3 ls**

![](/Assets/HTB/THREE/assets/upload.png)

![](/Assets/HTB/THREE/assets/lsls.png)
























