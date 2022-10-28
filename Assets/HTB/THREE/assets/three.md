# HTB(Three-Linux) 

![](/Assets/HTB/THREE/assets/three.jpg) 

# Summary 

* in this Box will new some steps in *cloud pentesting* and will know about *Amazon S3* and how we can know about its contents and how make our machine contact easily with it. 

# NMAP
-----
┌──(root㉿kali)-[~]
└─# nmap -sV  10.129.10.31                                           
Starting Nmap 7.92 ( https://nmap.org ) at 2022-10-28 14:38 EDT
Nmap scan report for 10.129.10.31
Host is up (0.24s latency).
Not shown: 998 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.7 (Ubuntu Linux; protocol 2.0)
80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 17.67 seconds
zsh: segmentation fault  nmap -sV 10.129.10.31


