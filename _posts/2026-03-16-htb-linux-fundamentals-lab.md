---
title: "HackTheBox Beginner Labs: My First Linux Box Walkthrough"
date: 2026-03-16
categories: [cybersecurity]
---

This article details my process and recommendations for completing the HackTheBox Linux Fundamentals lab which can be used a tutorial and learning guide for others to follow along as well. 

<h2>Introduction</h2>

HackTheBox is a learning platform aimed at teaching hands-on cybersecurity skills and knowledge. The content ranges in difficulty from beginner skills to advanced labs and capture-the-flag (CTF) challenges. The Linux Fundamentals lab module is one of the commonly completed first steps on a user's cybersecurity journey. This module includes foundational theory about the Linux operating system, it's structure and usage as well as providing overviews of common tools, how to install them and further topics to learn. The module also includes several quizzes/challenges for users to complete as they progress through the material. Even for users that come with pre-existing Linux skills, this lab is a valuable source to utilize as it also teaches and challenges more advanced Linux skills, briefly details core operating systems theory and provides beneficial overviews of further tools and skills every cybersecurity professional needs to learn eventually.

In this article, I will detail my process for completing the lab challenges along with my approach and recommendations to begin the shift from thinking like a student to thinking like a cybersecurity professional. I strongly suggest that anyone completing this module should keep a document for taking important notes about the theory presented as well as documenting their own process and results. Documenting my process as I completed each task served as a valuable learning tool upon completion as I was able to clearly see what I tried, what the result was, and then figure out why it did or didn't work. The most important advice I can give to anyone following along is to document their process in a similar manner because it is one of the best ways to improve specific skills faster!

**Important Note:** There are many similar articles online that detail alternative solutions to the same questions. There are two main reasons why my solutions may appear different from others:

1. Linux is not a "one size fits all" system. It may be possible that the same information can be found using a variety of commands or tools, so solutions will vary based on different approaches. 

2. I decided to complete this lab without looking at any other existing solutions because I wanted to fully challenge my own learning and abilities. Therefore, my provided solutions may not necessarily be the "best" or "most efficient" approach, but as this was an opportunity for me to experiment and grow, I completed it with the pure determination to solve the challenges on my own. After all, there may not even be existing solutions to search for when tackling problems in the professional cybersecurity world! You must rely on your own skills and the best way to learn how to do this is to treat every practice exercise as if you are already an industry professional. 

<h2>Tools Used</h2>

- [VirtualBox](https://www.virtualbox.org/)

- [Parrot OS Security](https://parrotsec.org/download/)

- [HackTheBox Linux Fundamentals](https://academy.hackthebox.com/course/preview/linux-fundamentals)

<h2>Process</h2>

In order to do the lab challenges, we must connect to HackTheBox. This can be done by either connecting through the browser and using the Pwnbox machine, or connecting via VPN through your own VM. 

<h3>Connect to HTB using VPN</h3>

It is easiest to complete this step by logging into HackTheBox from within your VM.

1. Once you have navigated to the module and are ready to start completing challenges, switch to the tab called "VPN" in the interactive area near the bottom of the page where the questions appear. You must select a VPN file to download. Generally, you can select the recommended one to use. 

2. Next, click on the button that says "Spawn the target system". This button starts an instance and provides you with the target IP address you will use to complete the challenges. 

3. Using your terminal, navigate to the directory where the VPN file is located. For most people this will be in `Downloads/` unless you have moved it elsewhere. Depending on the system or VPN file, the command to start the VPN might look different. Here is an example of what it should look like (or similar to):

    ```bash
    sudo openvpn academy-regular.ovpn
    ```

4. Once the VPN has successfully connected, leave the terminal window open for the duration of the challenges. 

5. In a new terminal window, you must now connect to HTB using the following command, making sure to replace `[IP address]` with the given target IP:

    ```bash
    ssh htb-student@[IP address]
    ```

6. Once prompted enter the given password for the lab as listed on Question 1 and you will be connected and ready to start!

<h3>Connect to HTB using Pwnbox</h3>

1. Once you have navigated to the module and are ready to start completing challenges, switch to the tab called "Pwnbox" in the interactive area near the bottom of the page where the questions are located. To start the Pwnbox machine, simply click the button that says "Start Pwnbox". 

2. Next, click on the button that says "Spawn the target system". his button starts an instance and provides you with the target IP address you will use to complete the challenges. 

3. After the target system has started, you are ready to go! There is no need to ssh or login to the `htb-student` account as Pwnbox is already set up to do this for you. 

Note: Below, I only include the sections which had questions to answer. Other sections that only contain theory or optional extra skills practice will not appear below, but are still worth looking at independently. I will also only include screenshots in the results below that do not explicitly give the exact solution after a command is run, to keep the challenge fun!

<h3>Section 6: System Information</h3>

---

**Question 1:** Find out the machine hardware name and submit it as the answer.

Tip: If you get stuck, read through the material again and then ask yourself if there was any information provided that might be useful here in solving this problem. 

Command used: `uname -r`

Result:

![htb_linux_fundamentals_q1](/images/htb_linux_fundamentals_q1.png)

**Answer:** <span class="reveal-answer">x86_64</span>

**Question 2:** What is the path to the htb-student's home directory?

Command used: `pwd`

**Answer:** <span class="reveal-answer">/home/htb-student</span>

**Question 3:** What is the path to the htb-student's mail?

Command used: `env`

Result:

![htb_linux_fundamentals_q3](/images/htb_linux_fundamentals_q3.png)

**Answer:** <span class="reveal-answer">/var/mail/htb-student</span>

**Question 4:** Which shell is specified for the htb-student user?

Command used: used same result from Question 3 (no new input)

Result:

![htb_linux_fundamentals_q4](/images/htb_linux_fundamentals_q4.png)

**Answer:** <span class="reveal-answer">/bin/bash</span>

**Question 5:** Which kernel release is installed on the system? (Format: 1.22.3)

Command used: `uname -r`

**Answer:** <span class="reveal-answer">4.15.0</span>

**Question 6:** What is the name of the network interface that MTU is set to 1500?

Command used: `ifconfig`

Result:

![htb_linux_fundamentals_q6](/images/htb_linux_fundamentals_q6.png)

**Answer:** <span class="reveal-answer">ens192</span>

<h3>Section 7: Navigation</h3>

---

**Question 1:** What is the name of the hidden "history" file in the htb-user's home directory?

Command used: `ls -la`

Result:

![htb_linux_fundamentals_q7](/images/htb_linux_fundamentals_q7.png)

**Answer:** <span class="reveal-answer">.bash_history</span>

**Question 2:** What is the index number of the "sudoers" file in the "/etc" directory?

Command used: `ls -li /etc`

Result:

![htb_linux_fundamentals_q8](/images/htb_linux_fundamentals_q8.png)

**Answer:** <span class="reveal-answer">147627</span>

<h3>Section 8: Working with Files and Directories</h3>

---

**Question 1:** What is the name of the last modified file in the "/var/backups" directory?

Command used: `ls -lt /var/backups`

Result:

![htb_linux_fundamentals_q9](/images/htb_linux_fundamentals_q9.png)

**Answer:** <span class="reveal-answer">apt.extended_states.0</span>

**Question 2:** What is the inode number of the "shadow.bak" file in the "/var/backups" directory?

Command used: `ls -li /var/backups`

Result:

![htb_linux_fundamentals_q10](/images/htb_linux_fundamentals_q10.png)

**Answer:** <span class="reveal-answer">265293</span>

<h3>Section 10: Find Files and Directories</h3>

---

**Question 1:** What is the name of the config file that has been created after 2020-03-03 and is smaller than 28k but larger than 25k?

Command used: `find / -type f -name *.conf -size +25k -size -28k -newermt 2020-03-03 -exec ls -al {} \; 2>/dev/null`

Result:

![htb_linux_fundamentals_q11](/images/htb_linux_fundamentals_q11.png)

**Answer:** <span class="reveal-answer">00-mesa-defaults.conf</span>

**Question 2:** How many files exist on the system that have the ".bak" extension?

Command used: `locate *.bak -c`

**Answer:** <span class="reveal-answer">4</span>

**Question 3:** Submit the full path of the "xxd" binary.

Command used: `which xxd`

**Answer:** <span class="reveal-answer">/usr/bin/xxd</span>

<h3> Section 11: File Descriptors and Redirections</h3>

---

**Question 1:** How many files exist on the system that have the ".log" file extension?

Command used: `find / -name *.log 2>/dev/null | wc -l`

**Answer:** <span class="reveal-answer">32</span>

**Question 2:** How many total packages are installed on the target system?

Tip: For this question, I had remembered often seeing packages listed with `dpkg`, so this was my starting point. Since I wasn't sure what command options were available, I typed `compgen -cv` to get a list of commands available. I saw `dpkg` in this list, so I next typed `dpkg --help` to see what specific commands were available for packages. I then tried one of the listed options and typed `dpkg --get-selections` but noticed it returned a list with packages marked "install" or "deinstall". Since this question specifically asked for the number of installed packages, I used grep to help filter the results and `wc -l` to cound them.

Command used: `dpkg --get-selections | grep -w "install" | wc -l`

**Answer:** <span class="reveal-answer">737</span>

<h3>Section 12: Filter Contents</h3>

---

**Question 1:** How many services are listening on the target system on all interfaces? (Not on localhost and IPv4 only)

Tip: For this question, I knew I had to use `netstat` but I wasn't sure exactly what command options to use. So, I started with `netstat --help` and saw that I could list and specify by IPv4. I tried this by typing `netstat -4 -l` and saw that within the returned output was the answer I was looking for. However, the output also had other information that I did not need for this question, so again I used grep to filter the results and `wc -l` to count them.

Command used: `netstat -4 -l | grep "LISTEN" | grep -v "localhost" | wc -l`

**Answer:** <span class="reveal-answer">7</span>

**Question 2:** Determine what user the ProFTPd server is running under. Submit the username as the answer.

Tip: I was not sure where to start for this question, so I first typed `locate proftpd`. This did not give me the information I needed. So, I tried `type proftpd` and the resuling output said that "proftpd is hashed", which typically indicates that it is a command. Next, I simply typed `proftpd` and saw `/etc/proftpd/proftpd.conf` in the output. I decided to try using cat on this file, which then gave the specific information I needed.

Command used: `cat /etc/proftpd/proftpd.conf`

Result:

![htb_linux_fundamentals_q17](/images/htb_linux_fundamentals_q17.png)

**Answer:** <span class="reveal-answer">proftpd</span>

**Question 3:** Use cURL from your Pwnbox (not the target machine) to obtain the source code of the "https://www.inlanefreight.com" website and filter all unique paths (https://www.inlanefreight.com/directory" or "/another/directory") of that domain. Submit the number of these paths as the answer.

Tip: For this question, I knew that I wanted to filter the answers to only include the URLs that belonged to "https://www.inlanfreight.com". I had to find a way to filter each URL until it reached the end of the URL. First, I included `-o` in the grep command which tells it to get the whole specified text. However, I knew that if I just used grep on this that it wouldn't return everything I needed because the URL paths are not all the same length. So, I also included `[^\"']*` as part of the command to solve this problem. The `[]` define the character set I wanted grep to use. The `^` when it is inside of the brackets tells grep NOT. In this case, I wanted grep to match any character that is NOT a single quote or a double quote because in HTML, URLs are either enclosed with single quotes or double quotes. Lastly, the `*` tells grep to repeat it zero or more times. In this case, this means repeat it until it matches a character that is a single or double quote. Next, I used `sort -u` to filter only the unique URLs to make sure that duplicates do not get counted in the result. I then used `wc -l` to count the results.

Command used: `curl https://www.inlanefreight.com | grep -o "https://www.inlanefreight.com/[^\"']*" | sort -u | wc -l`

**Answer:** <span class="reveal-answer">34</span>

<h3>Section 15: User Management</h3>

---

**Question 1:** Which option needs to be set to create a home directory for a new user using "useradd" command?

Command used: `useradd --help`

**Answer:** <span class="reveal-answer">-m</span>

**Question 2:** Which option needs to be set to lock a user account using the "usermod" command? (long version of the option)

Command used: `usermod --help`

**Answer:** <span class="reveal-answer">--lock</span>

**Question 2:** Which option needs to be set to execute a command as a different user using the "su" command? (long version of the option)

Command used: `su --help`

**Answer:** <span class="reveal-answer">--command</span>

<h3>Section 17: Service and Process Management</h3>

---

**Question 1:** Use the "systemctl" command to list all units of services and submit the unit name with the description "Load AppArmor profiles managed internally by snapd" as the answer.

Command used: `systemctl list-units --type=service`

Result:

![htb_linux_fundamentals_q19](/images/htb_linux_fundamentals_q19.png)

**Answer:** <span class="reveal-answer">snapd.apparmor.service</span>

<h3>Section 18: Task Scheduling</h3>

---

**Question 1:** What is the Type of the service of the "dconf.service"?

Tip: For this question, I first typed `locate dconf.service` which returned the path of the file. Even though the path already gave an indication of the answer, to make sure I used cat on the file to see that the service was in fact correct.

Command used: `cat /usr/share/dbus-1/services/ca.desrt.dconf.service`

**Answer:** <span class="reveal-answer">dbus</span>

<h3>Section 20: Working with Web Services</h3>

---

**Question 1:** Find a way to start a simple HTTP server inside Pwnbox or your local VM using "npm". Submit the command that starts the web server on port 8080 (use the short argument to specify the port number).

Tip: For this question, i used Pwnbox and first had to do `sudo npm install -g http-server` after doing research about what I needed to install. After some experimentation, I also learned that it was only possible to do this with sudo included due to the permissions configurations for the Pwnbox machine. 

**Answer:** <span class="reveal-answer">http-server -p 8080</span>

**Question 2:** Find a way to start a simple HTTP server inside Pwnbox or your local VM using "php". Submit the command that starts the web server on the localhost (127.0.0.1) on port 8080.

Tip: For this question I first typed `php --help` to see what syntax was required. This command returned specific information about how to start the web server with the following syntax: `php -S <addr>:<port>`.

**Answer:** <span class="reveal-answer">php -S 127.0.0.1:8080</span>

<h3>Section 22: File System Management</h3>

---

**Question 1:** How many partitions exist in our Pwnbox? (Format: 0)

Command used: `sudo fdisk -l`

**Answer:** <span class="reveal-answer">3</span>

<h2>Challenges & Lessons Learned </h2>

- When unsure of where to start, it can be helpful to ask "what do I need to find?" or "what does the expected output need to do?"

- It can be tempting just to search for the answers or solutions to problems right away. However, it can be more beneficial to try figuring it out on your own first. A good place to start is by using the `--help` or `-h` command option or `man <command>` to access the manual pages for a command. These tricks can provide helpful information such as syntax and descriptions of what commands do. This is how to train your brain to think like a cybersecurity professional! Only obtaining the "correct" answer will not benefit you in the long run if you do not understand how or why you are doing something. 

- There is often more than one way to obtain the information you are looking for when working within the Linux environment. 

- Filtering tools like grep, cut, tr, column, awk, wc and sed are extremely useful for outputing the exact information you need. This can save time by eliminating the need to manually sort or count results or by outputting results in an easy to read format. 

- Aside from just navigating files and directories, there are many features/tools in Linux that you can use to accomplish other tasks such as creating containers, configuring networks, setting up firewall and security protocols, using remote desktops and more!

<h2>Next Steps</h2>

- Complete [HackTheBox Introduction to Networking](https://academy.hackthebox.com/course/preview/introduction-to-networking) module.

- Complete [HackTheBox Nmap Enumeration Lab](https://academy.hackthebox.com/course/preview/network-enumeration-with-nmap)