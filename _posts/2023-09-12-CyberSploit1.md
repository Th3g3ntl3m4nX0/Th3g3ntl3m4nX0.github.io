---


title: "CyberSploit1 "
date: 2023-9-12 
img_path: ../../assets/image
image: banner.png
categories: [Proving grounds, Easy,Privesc]
tags: [ctf, nmap, base64, enumeration, gobuster, exploitDB, ssh]     # TAG names should always be lowercase


---



> **[Cybersploit1](https://portal.offsec.com/labs/play)**  is a boot2root VM from Offsec Proving Grounds. it's also a fairly simple linux box. We shall start with `nmap` scan to see the ports open on the machine. We will later  use `gobuster` for directory brute force and from there we would find where you can get something interesting to gid deeper. So we shall login with `SSH`  which will give us the initial access to the system. Finally we shall do privilege escalation by uploading the 'overlayfs' Local Privilege Escalation  exploit from `ExolitDB` to get root privileges.
{: .prompt-tip }

`Ready, set, pwn!` 


## Scanning and enumeration

I started the reconnaissance by running a port scan with Nmap, checking default scripts and testing for vulnerabilities.  We have used -sC for default 
scripts, -sV to enumerate all versions, -oA to output all format in a file called initial and finally it’s IP address. Here is the results:

```shell

┌──(root㉿kali)-[~]
└─$ nmap -sC -sV -oA initial 192.168.155.92 
Starting Nmap 7.94 ( https://nmap.org ) at 2023-09-12 11:44 EAT
Nmap scan report for 192.168.155.92
Host is up (0.20s latency).
Not shown: 998 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 5.9p1 Debian 5ubuntu1.10 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   1024 01:1b:c8:fe:18:71:28:60:84:6a:9f:30:35:11:66:3d (DSA)
|   2048 d9:53:14:a3:7f:99:51:40:3f:49:ef:ef:7f:8b:35:de (RSA)
|_  256 ef:43:5b:d0:c0:eb:ee:3e:76:61:5c:6d:ce:15:fe:7e (ECDSA)
80/tcp open  http    Apache httpd 2.2.22 ((Ubuntu))
|_http-server-header: Apache/2.2.22 (Ubuntu)
|_http-title: Hello Pentester!
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 17.54 seconds.

```
                                                            
  We see `ssh` port 22 open and `http` port 80 open which is running an Apache 2.2.22 web server.                                                           


  Looking at port 80 on the web browser, we see a GIF. 
  ![image](/assets/image/pic1.png)

  Looking at the page source, I found a username `itsskv`. This might be useful later on!
  ![image](/assets/image/pic2.png)
