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

`Ready, set, pwn`!` 
