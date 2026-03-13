---
title: "Getting Started with Linux: My First Commands and Lessons Learned"
date: 2026-03-10
categories: [cybersecurity]
---

This article explores setting up introductory cybersecurity learning environments and how to use them. 

<h2>Introduction</h2>

Learners new to the field of cybersecurity are faced with many tools and learning platforms to choose from. Without creating a plan to properly set up suitable learning environments for exploring these tools, learners can get overwhelmed.

The goal of this article is to share the plan I created for setting up my cybersecurity learning environments and becomming familiar with some tools so that others can follow along as well. However, it is important to note that individual discretion must be applied as not all tools and/or platforms may be suitable for an individual's specific project or learning goals.

<h2>Tools Used</h2>

- [Parrot OS Security](https://parrotsec.org/download/)

- [VirtualBox](https://www.virtualbox.org/)

- [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

- [HackTheBox Academy](https://academy.hackthebox.com/)

- [TryHackMe](https://tryhackme.com/)

<h2>Process</h2>

1. Install Parrot OS Security on VirtualBox or the VM (Virtual Machine) of your choice. 

    1.1. It may be useful to start with [Ubuntu](https://ubuntu.com/download/desktop) for basic exercises if unfamiliar with Linux systems. 

    1.2. If more guidance is needed, follow the [GeeksforGeeks tutorial](https://www.geeksforgeeks.org/installation-guide/how-to-install-parrot-os-in-virtualbox/).

2. Install Git and set up [GitHub repo](https://docs.github.com/en/repositories/creating-and-managing-repositories/quickstart-for-repositories) for storing projects.

3. Learn basic linux commands: cd, ls, pwd, chmod

    3.1. Although this information is available in many places, it may be helpful to follow a guided [tutorial](https://ryanstutorials.net/linuxtutorial/) that provides more in-depth information. 

4. Explore networking basics: ping, ip addr

    4.1. Although this information is also available in many places, it may again be helpful to follow a [tutorial](https://www.geeksforgeeks.org/computer-networks/computer-network-tutorials/) for more structured learning.

5. Sign up for the [HackTheBox Linux Fundamentals lab](https://academy.hackthebox.com/course/preview/linux-fundamentals) or alternatively the [TryHackMe Linux Fundamentals Course](https://tryhackme.com/module/linux-fundamentals).

<h2>Challenges & Lessons Learned </h2>

- Installing Parrot OS on VirtualBox:

    - Some modules on HackTheBox recommend configuring the system by choosing to encrypt it and selecting Swap (No Hibernate) before running your VM for the first time. 

    - If errors occur during installation, it may be necessary to increase the allocated memory and/or CPU cores for your VM.

    - Parrot OS Security (or Kali Linux) are good systems to start with because they come with pre-installed security tools that you will likely need to use as your cybersecurity learning continues.

- Becoming familiar with basic linux commands:

    - cd (change directory): helps you move around your system to different locations.

    - ls (list): displays a list of contents in your current directory. 

    - pwd (print working directory): displays where you are currently located in your system.

    - chmod (change mode): modify file system permissions. 

- Explore networking basics:

    - ping: tests connectivity, measures round-trip time for packets traveling between devices and identifies packet losses as well as other issues. 

    - ip addr: an identifying label for devices within a network and/or the internet.

<h2>Next Steps</h2>

- Practice HackTheBox Linux Fundamentals lab tasks. 

- Intro to networking: learn about TCP/IP, ports, nmap scans.