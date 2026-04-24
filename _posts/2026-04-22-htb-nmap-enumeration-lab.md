---
title: "HackTheBox Network Enumeration with Nmap: Lab Walkthrough"
date: 2026-04-22
categories: [cybersecurity]
---

This article details my process and recommendations for completing the HackTheBox Network Enumeration with Nmap lab which can be used as a tutorial and learning guide for others to follow along as well.

<h2>Introduction</h2>

In my [previous article](/cybersecurity/networking-fundamentals-post/), I talked about how cybersecurity issues are fundamentally networking issues and why it is important to learn the basic foundations of networking concepts. However, just as it is important to understand the theory behind cybersecurity topics, it is also important to have a solid toolbox of skills that you are ready to put to use as needed. After all, it wouldn't be very helpful to have a box of tools if you didn't know how or when to use them when a situation arises! One such tool that every cybersecurity professional should have is called Nmap, which stands for "Network Mapper". Nmap is a tool that allows you to analyze and audit networks by identifying hosts, scannings ports and much more! The Network Enumeration with Nmap lab is a popular beginner skills lab on the HackTheBox learning platform that teaches the essential theory behind the Nmap tool as well as providing simulated environments for practicing how to use it. I would recommend this lab to anyone wanting to further build their foundational skills as I felt highly prepared and confident in my understanding of Nmap upon completion of the module. Aside from that, the rigor of the challenges also made it a fun and rewarding experience in the process! 

In this article, I will detail my process for completing the lab challenges as well as providing my own tips and insights I gained while completing the module. Throughout the activities, I kept a notes document in which I wrote down useful information and detailed my steps and thinking, and I would advise anyone else following along to do the same. Keeping track of this information proved to be a valuable resource as it helped me identify next steps to take when I got stuck (even if those steps turned out to be me going down the wrong path) and prevented me from going in circles and trying things over and over that didn't work. Despite there being other similar walkthroughs online, I decided to fully challenge myself on this lab activity as I have previously done for others, and try to solve the challenges entirely on my own. I chose to do this because my ongoing goal is push myself to think like a cybersecurity professional test my ideas in an environment where it is both beneficial and safe to make mistakes. I believe doing so will better prepare me to face difficult problems in professional settings as learning from mistakes is one of the most powerful ways to improve your understanding and skillset. You can follow or adapt the problem solving process I used for tricky challenges as follows:

1. What information do I already have or know? 

2. Can this information help me find what I am looking for?

3. What other informatin could possibly be relevant or useful in finding a direction or next step to take?

    - For instance, say you are looking for information regarding a specific web service but are completely stuck on what to do. It might be helpful to take a step back and think "what information do I know about web services?". This might help you remember (or conduct research to find) that port 80 is typically used for web servers/web traffic, so maybe seeing what you can find regarding port 80 would be a good first step. If you are stuck, don't be afraid to work backwards!

4. If something I tried didn't work, is there any information in the results that can give me an idea of what to try instead? 

5. Is the information or context I need something that could be found in the man pages or by using help commands? 

**Disclaimer:** As mentioned before, you may find that similar articles online or even your own solutions, appear differently from my own. Remember that this is normal and expected as Linux and its tools are not a "one size fits all system". There are often many approaches that can be taken to obtain the same results. 

<h2>Tools Used</h2>

- [VirtualBox](https://www.virtualbox.org/)

- [Parrot OS Security](https://parrotsec.org/download/)

- [HackTheBox Network Enumeration with Nmap](https://academy.hackthebox.com/course/preview/network-enumeration-with-nmap)

- [Nmap](https://nmap.org/)

<h2>Process</h2>

In order to do the lab challenges, we must connect to HackTheBox. If you are unsure how to do this, you can check out my [Linux Fundamentals Lab](/cybersecurity/htb-linux-fundamentals-lab/) article which provides a detailed walkthrough of how to connect.

Note: Below, I only include the sections which had questions to answer. Other sections that only contain theory or optional extra skills practice will not appear below, but are still worth looking at independently. I will also include screenshots in the results below for questions that required using commands to answer.

**Important:** For any commands provided below, remember to replace `<target>` with the actual target IP you are provided to work with.

<h3>Section 3: Host Discovery</h3>

--- 

**Question 1:** Based on the last result, find out which operating system it belongs to. Submit the name of the operating system as result.

**Tip:** This question does not require you to connect to HackTheBox and perform any commands. The information you need to answer the question is provided in the content example results. The given hint also directs you towards the Time-To-Live (TTL) value, indicating that this might be important information. If you are still stuck, it might be helpful to do some research about different TTL values and which operating systems they typically are associated with. 

**Answer:** <span class="reveal-answer">windows</span>

<h3>Section 4: Host and Port Scanning</h3>

---

**Question 1:** Find all TCP ports on your target. Submit the total number of found TCP ports as the answer.

**Tip:** Always make sure you are using the correct target IP that is spawned for the machine when answering questions and that you are not using any old IPs. This HackTheBox lab is marked as easy, so you should be able to very clearly obtain results with ports marked as "OPEN". If not, you should reset your VPN connection or the Pwnbox machine. When I first worked on this question, I was not obtaining a single port that was "OPEN" which resulted in me doing lots of in-depth research about Nmap commands and trying advanced tactics, thinking it was supposed to be this difficult. I didn't realize until later that this task was not, in fact, supposed to be this hard and that my VPN wasn't properly connected (a rookie mistake)! This experience did, however, benefit me because by the time I reached the hard lab I felt thoroughly prepared and knowledgeable about what to do. 

First, I tried the command: `sudo nmap <target> -p- --open -n -Pn --min-rate 1000`

This returned the list of open ports:

![htb_nmap_lab_q1](/images/htb_nmap_lab_q1.png)

In this case, you could count the results by hand, but it is more practical to use filtering tools to do it for you because sometimes you may receive very many results that would be too tedious to count by hand. 

Command used: `sudo nmap <target> -p- --open -n -Pn --min-rate 1000 | grep open | wc -l`

**Answer:** <span class="reveal-answer">7</span>

**Question 2:** Enumerate the hostname of your target and submit it as the answer. (case-sensitive)

Command used: `sudo nmap <target> -n -Pn -sV`

Result:

![htb_nmap_lab_q2](/images/htb_nmap_lab_q2.png)

**Answer:** <span class="reveal-answer">NIX-NMAP-DEFAULT</span>

<h3>Section 5: Saving the Results</h3>

---

**Question 1:** Perform a full TCP port scan on your target and create an HTML report. Submit the number of the highest port as the answer.

I completed this question in several steps. 

First, I did the port scan: `sudo nmap <target> -p- -Pn -n --min-rate 1000 -oX target`

The `--min-rate 1000` part speeds up the process, the `-oX` part tells Nmap to save the results as XML output, and `target` is the name of the result file I specified. 

Then, I converted the XML file to HTML report type: `xsltproc target -o target.html`

Lastly, I opened the report in the Firefox browser to see the results: `firefox target.html`

This trick displays the results of the scan in an organized, readable format in your browser. Once the page is opened, the answer will appear in a table that should look something like this:

![htb_nmap_lab_q3](/images/htb_nmap_lab_q3.png)

**Answer:** <span class="reveal-answer">31337</span>

<h3>Section 6: Service Enumeration</h3>

---

**Question 1:** Enumerate all ports and their services. One of the services contains the flag you have to submit as the answer.

First, I did a scan: `sudo nmap <target> -p- -sV -Pn`

**Tip:** The `-p-` part tells Nmap to scan all ports (it often defaults to only scanning the first 1000 ports). After getting the results, I decided to approach this problem by choosing a port to look at that is not very common. In this case, I chose port 31337. 

Then, I used netcat to manually connect in order to grab the banner, which Nmap did not provide. 

Command used: `nc -nv <target> 31337`

Result (target IP covered with white box as this will vary for each person):

![htb_nmap_lab_q4](/images/htb_nmap_lab_q4.png)

**Note:** Since this is a HackTheBox activity, the result seen next to 220 is the Capture The Flag (CTF) style answer that the question is looking for. However, if you did this command in another situation, you might see something that looks like: `220 FTP Server ready` instead.

**Answer:** <span class="reveal-answer">HTB{pr0F7pDv3r510nb4nn3r}</span>

<h3>Section 7: Nmap Scripting Engine</h3>

---

**Question 1:** Use NSE and its scripts to find the flag that one of the services contain and submit it as the answer.

First, I tried: `sudo nmap <target> -A --min-rate 1000`

Result:

![htb_nmap_lab_q5p1](/images/htb_nmap_lab_q5p1.png)

**Tip:** For HackTheBox challenges like this, it is unlikely that the new flag you are looking for will be in the same location as the previous flag, so this is an indication that it might be best to start somewhere else. 

Based on these results, my intuition was telling me to look at ports 22 and 80. 

I started with port 22 and tried: `sudo nmap <target> -p 22 --script default,safe,discovery`

I wasn't sure if the results were meaningful or not, so I thought maybe I had to be more specific. Since port 22 was shown as SSH, I decided to see if there were any scripts I could use that were SSH specific. I ran: `nmap --script-help ssh-*` which returned SSH scripts that I could run. 

**Tip:** If you are ever unsure of what scripts are available, you can type: `nmap --script-help <category>` and it will return a list of scripts you can use that fall within that specific scripting category and a description of what they do. If you want to be more detailed and find a list of options that are related to a specific script option you can run: `nmap --script-help <script_option>-*` instead, and Nmap will only return a list of related scripts. Also, if you do: `sudo nmap <target> --script=<script_option>-*` it will automatically run every available script that is related to the given option. 

Next, I tried: `sudo nmap <target> -p 22 --script ssh-hostkey,ssh-auth-methods,ssh2-enum-algos` 

This result still didn't return anything that seemed particularly meaningful, so I decided to look at port 80 instead. 

After the initial scan, the results showed that port 80 was using HTTP with Apache, so I looked for scripts that were either related to HTTP or related to Apache. Instead of running every HTTP script, I tried to find ones that I thought could potentially be useful for this specific situation and found the following: `http-apache-server-status, http-comments-displayer, http-ls, http-auth, http-userdir-enum`. I ran the scan using these scripts and wasn't able to find anything specifically showing the answer but it was starting to seem like I was going in the right direction. 

Then, I looked at the list of script options again and ran the ones I thought could potentially help and I kept trying this process until I found: `http-enum`.

I ran the command: `sudo nmap <target> -p 80 --script http-enum`

Result:

![htb_nmap_lab_q5p2](/images/htb_nmap_lab_q5p2.png)

This result returned a file called `robots.txt` which I had definitely seen before already after trying some of the more general script options. I decided to try to look at what was in this file, which ended up returning the flag I was looking for.

Command used: `curl http://<target>/robots.txt`

**Answer:** <span class="reveal-answer">HTB{873nniuc71bu6usbs1i96as6dsv26}</span>

<h3>Section 10: Firewall and IDS/IPS Evasion - Easy Lab </h3>

---

For the last three labs, we are given the following scenario: we have been hired by an IT company to test their security defenses which includes their IDS (Intrusion Detection Systems) and IPS (Intrusion Prevention Systems). After each test, the company wants to improve their security but we will not know what guidelines they will use when these changes are made. We are provided with a machine to test and given access to a site that monitors our network noise. If we reach a certain number of alerts, we will be banned from the system, so we must perform the tests as quietly as possible. 

**Question 1:** Our client wants to know if we can identify which operating system their provided machine is running on. Submit the OS name as the answer.

First, I tried: `sudo nmap <target> -n -Pn -O -T2`

Results:

![htb_nmap_lab_q6p1](/images/htb_nmap_lab_q6p1.png)

**Tip:** Using the command with `-O` returns several guesses for Linux but IDS/IPS systems can be set up to intentionally make this too vague, and HackTheBox wants a specific answer for this question. Also, using less agressive scan speeds like `-T2` can prevent overloading the network which can help evade detection and getting banned.

Command used: `sudo nmap <target> -n -Pn -p 80 -sV -T2`

Result:

![htb_nmap_lab_q6p2](/images/htb_nmap_lab_q6p2.png)

This result returned Apache version ((Ubuntu)) as one of the services, which can be a good indicator because some software versions are bundled to specific operating systems. 

**Answer:** <span class="reveal-answer">Ubuntu</span>

<h3>Section 11: Firewall and IDS/IPS Evasion - Medium Lab </h3>

---

Scenario: After the first test, the client administrators updated their IDS/IPS and firewall. We could hear that some of them were unsatisfied with the previous configurations during the meeting and they could see that the network traffic could be filtered more strictly. 

We are also told that we must use the UDP protocol on the VPN for this question. 

Hint: During the meeting, we could hear the administrators talking about the host we tested as a publicly accessible server that was not mentioned before. 

**Question 1:** After the configurations are transferred to the system, our client wants to know if it is possible to find out our target's DNS server version. Submit the DNS server version of the target as the answer.

We are already told that we must use the UDP protocol and we know that the administrators were talking about publicly accessible servers. So, we can use the well-known fact that port 53 typically uses UDP to manage DNS queries, which is essential for users to be able to do things like access web browsers, email and locating servers. This already gives us a very good indication of what to do. 

First, I decided to look for specific NSE scripts that could help find the exact information I was looking for and I decided to use: `dns-nsid`.

Command used: `sudo nmap <target> -Pn -sU -p53 -T2 --script dns-nsid`

Number of alerts triggered from this command: 2 (excellent!)

Result:

![htb_nmap_lab_q7](/images/htb_nmap_lab_q7.png)

**Answer:** <span class="reveal-answer">HTB{GoTtgUnyze9Psw4vGjcuMpHRP}</span>

<h3>Section 12: Firewall and IDS/IPS Evasion - Hard Lab </h3>

---

Scenario: After the second test, the client sent one of their administrators to a training course for IDS/IPS systems. After the training, the client wants us to test the system again because the specific services must be changed, and the communication for the provided software had to be modified. 

Hint: The client also mentioned that they were forced to add a service that plays a vital role for their customer because they require large amounts of data. 

**Question 1:** Now our client wants to know if it is possible to find out the version of the running services. Identify the version of service our client was talking about and submit the flag as the answer.

Immediately, I knew that because the services had to be changed, I should try to figure out what the new service was that had to be added. Intuitively, I knew that I should be looking for a new service or port that appears that indicates data storage because of the given hint. 

First, I ran: `sudo nmap <target> -p- -sS -sV -Pn -n --disable-arp-ping --source-port 53`

Number of alerts triggered from this command: 18 (not too bad)

**Tip:** Use source port 53 because it commonly tricks firewalls into allowing scan traffic to impersonate legitimate DNS responses and admins often misconfigure firewalls to allow all incoming UDP traffic from port 53 to allow DNS replies into the network. 

Result:

![htb_nmap_lab_q8p1](/images/htb_nmap_lab_q8p1.png)

After this scan, I was able to see that the new port that appeared was port 50000 and the service was listed as `tcpwrapped` which typically indicates we are being blocked by the firewall. 

I searched online what port 50000 is used for and found that it is typically the default TCP port for IBM DB2 database instances. Since we know that our client needs to handle large amounts of data, this is the likely the port we want to evaluate and find the version of. 

Command used: `sudo nc -nv -p 53 <target> 50000` 

**Tip:** Some users, including myself, have difficulty running this command on Pwnbox machines and receive libsock/socket bind failures, which is supposedly because Pwnbox is already using this port to run the DNS service systemd-resolved. If you run this command with `sudo`, Pwnbox will tell you that this port is already in use. In this case, switch to your local VPN to do this part instead. 

Result:

![htb_nmap_lab_q8p2](/images/htb_nmap_lab_q8p2.png)

It worked, we found the flag!

**Answer:** <span class="reveal-answer">HTB{kjnsdf2n982n1827eh76238s98di1w6}</span>

<h2>Challenges & Lessons Learned </h2>

- When using Nmap Scripting Engine (NSE), use the `--script-help <category>` command to see a list of available scripts you can run within that category and a description of what they do. 

- Always make sure you are targetting the right IP or you might not be able to correctly find the results you are looking for. 

- If the output you get from a scan seems meaningful or suspicious, this is a good indication that you should evaluate this result deeper. 

- Use netcat to manually connect and scan specific ports, which can help identify connection issues or provide more information that Nmap might not be showing you. 

<h2>Next Steps</h2>

- Learn the basics of [cryptography in Python](https://realpython.com/courses/exploring-https-cryptography/)