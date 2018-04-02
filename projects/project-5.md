---
layout: project
type: project
image: images/kali2.jpg
title: Penetration Test Report
permalink: projects/pentest
date: 2018
labels:
  - Penetration Test
  - Kali Linux
  - Network Security
summary: Test the security of Machines through penetration.
---

  <img class="ui medium left floated image" src="../images/kali.png">


This project is a report on the exploitation of the four servers on a lab network, 
which I have been instructed to penetrate during the University of Hawaii at Manoa Penetration Testing Event.
This document identifies the vulnerabilities that have been 
discovered during this period of assessment, how the vulnerabilities had been discovered,and the
recommended steps needed to secure the systems.

## Objective
The objectives of this penetration are to capture the medal.txt and trophy.txt hash tables hidden within the servers.  These IP addresses are as follows:

10.1.1.11

10.1.1.12

10.1.1.13

10.1.1.14


## Requirements
Overall High-Level Summary and Recommendations (non-technical).
Methodology walkthrough and detailed outline of steps taken.
Each finding with included screenshots, walkthrough, sample code, and proof.txt if applicable.

## Examination Report – High-Level Summary
### Machine at Server 'A’ – 10.1.1.12:
medal.txt:
65ncQ4ljVXW16EgDCEi7

trophy.txt:
dhx9sV3y024DW86kMf2b

Got in through web application, server configurations, and lack of password security.

### Machine at Server 'B’ – 10.1.1.11:
medal.txt:
SSnsZw4pG2w8K05IYXE3

trophy.txt:
iy53KIjsxAAI0cICQewyp

Got in through lack of root password security at machine and sql database.

## Machine at Server 'C’ – 10.1.1.13:
medal.txt:
MENd1Gm7A0F95VbhdnCm

trophy.txt:
UGCortJUd1uDfZ00XSfv

Got in through files stored outside root browser on web.

## Machine at Server 'D’ – 10.1.1.14:
trophy.txt:
9h0WZA1E7YxY2AXFpeTV

Got in through social engineering the password.
	
## Examination Report - Recommendations
### Server ‘A’ - 10.1.1.12
Secure web application by removing user password from source code.

Update user password so that it is not ‘password’.

Remove or edit files holding passwords, including .bash_history.backup.

Update root password to another secure password, not saving it on file.

### Server ‘B’ - 10.1.1.11
Secure sql database and root login by changing password to a secure password.

Secure user passwords by not storing them on database.

### Server ‘C’ - 10.1.1.13
Secure critical files behind a login. 

Remove password files.

### Server ‘D’ - 10.1.1.14
Create a strong root password

## Examination Report – Methodologies
### Server ‘A’ - 10.1.1.12
After finding that there was a login page on the https url, I viewed the page source, where the words “username: webadmin // password: password” was easily seen. Using those credentials, I was able to login to the computer, and easily find medal.txt. After a search, I located .bash_history.backup, which stored a very obvious looking password ‘withgreatpowercomesgreatresponsibility’. That enabled me to access all the files and locate trophy.txt

### Server ‘B’ - 10.1.1.11
As there was a mysql, I managed to open it using the login ‘root’ and password ‘password’. I searched through the database and located a table called user_accounts. This table located the username ‘mount’ with password ‘mount’. I logged into the system using the user ‘mount’ and obtained medal.txt. I logged into the system using user ‘root’ and found trophy.txt.

### Server ‘C’ - 10.1.1.13
Upon locating the url of the index file, I managed to dig into the url until I located medal.txt. I then started my search again, looking at the main page, until I found the backup file. The backup file contained a hashed code with the administrator password. This password was then used to access the remote desktop and obtain trophy.txt.

### Server ‘D’ - 10.1.1.14
Upon locating the phpmyadmin file, the search for the password was implemented. Administrator keeps a profile picture of a Jigglypuff on chat media, which hinted the password to being ‘pokemon’. Upon the alteration of the password, the system crashed.

## Examination Report – Information Gathering
  During this penetration test, I was tasked with exploiting the examination lab network. The specific IP addresses were:
  
10.1.1.11

10.1.1.12

10.1.1.13

10.1.1.14


## Examination Report – Penetration
Deeper explanations of vulnerabilities exploited and the methods and tools used.
### Examination Report – 10.1.1.12 Server ‘A’ Penetration
Vulnerability Exploited:  W3C XHTML Ajax Security Breach

System Vulnerable: 10.1.1.12

Tools Selected: Local file execution, find
Vulnerability Explanation: W3C XHTML Ajax https url website contained a massive security breach with the inclusion of the login and password in the code comments. The code in .bash_history.backup contained the root password.

Vulnerability Fix: Reconfigure the website source code to remove the code comments. Remove access to the password from user files.

Severity: i.e. Critical

#### Procedure  

Step 1: View source code on https://10.1.1.12/login.

Step 2: Log into server using webadmin credentials and retrieve medal.txt.

Commands: 

rlogin -l webadmin 10.1.1.12

webadmin@10.1.1.12's password: password

webadmin@ajaxterm:~$ ls

availablecmds.txt  medal.txt

webadmin@ajaxterm:~$ cat medal.txt

65ncQ4ljVXW16EgDCEi7



Step 3: Search for files that may contain data.

Commands: 
ls -larth

Step 4: Open file to locate password.

Commands: 
cat .bash_history.backup

 Step 5: Log into root and search for trophy.txt
 
Commands: 

su root

Password: withgreatpowercomesgreatresponsibility

cd ../../../../../

find -name trophy.txt

cd ./root

cat trophy.txt


### Examination Report – 10.1.1.11 Server ‘B’ Penetration

Vulnerability Exploited:  Root login and SQL Database Password Exploit

System Vulnerable: 10.1.1.11

Tools Selected: Mysql, local file execution, Hash-identifier, find

Vulnerability Explanation: The root login was not configured, and the password was ‘password’. This enabled me to access the root directory, as well as the mysql database where another passsword was stored.

Vulnerability Fix: Set strong root password for the computer and the mysql database. Remove tables that contain passwords.

Severity: i.e. Critical

#### Procedure  
Step 1: As nmap showed that there was an open mysql, login root.

Commands: 

mysql -u root -p -h 10.1.1.11

Enter password: password

Step 2: Open database called ‘user_accounts’ to find username and password hashcode.

Commands: 

show database

use user_accounts

show tables;

select * from account_info

Step 3: Lookup password on google - hash password was ‘mount’.

Step 4: Login to computer with ‘mount’ credentials. Find Medal.txt.

Commands: 

rlogin -l mount 10.1.1.11

password: mount

cat medal.txt

Step 5: Login to root to locate trophy.txt.

Commands: 

su root

password: password

find -name trophy.txt

cat ./root/trophy.txt


### Examination Report – 10.1.1.13 Server ‘C’ Penetration
Vulnerability Exploited:  Directory Traversal of Unsanitized Url Field

System Vulnerable: 10.1.1.13

Tools Selected: Directory buster, hash-identifier, local file execution, rdesktop

Vulnerability Explanation: Http server had an unsanitized Url field which allowed Directory traversal. Within the unsecure directory medal.txt was located. Also hidden further in the directory was the hash password for the administrator login. Once that was identified, the remote desktop was accessible, and trophy.txt was located on the desktop.

Vulnerability Fix: Configure the Url to keep all directories locked. Remove the passwords from the directory. Update the Administrator password.

Severity: i.e. Critical

#### Procedure  
Step 1: Use Directory Buster on ip to locate index.html 

Commands: 

dirb http://10.1.1.13

    
Step 2: Traverse through the directory at index.html and retrieve medal.txt.


Step 3: Traverse through the rest of the directory and find backup file. 

Step4: Run Hash-identifier to crack code. Use code on rdesktop login.

Commands: 

rdesktop 10.1.1.13

login: Administrator

Password: bolo

### Examination Report – 10.1.1.14 Server ‘D’ Penetration
Vulnerability Exploited:  Social Engineering of Password

System Vulnerable: 10.1.1.12

Tools Selected: Directory Buster, PhpMyadmin, mysql, exploit 3274

Vulnerability Explanation: While the root password had been altered, it was an simple password that was exploited by means of social engineering. Once logged into Mysql, I allowed myself permission to access the database. This enabled me to give myself permissions to exploit the database as I opened up a shell using winufd.sql to retrieve the trophy.txt.

Vulnerability Fix: Remove all unauthorised permissions to Database. Update root password with a secure password.

Severity: i.e. Moderate

#### Procedure  
Step 1: Use Directory Buster on ip to locate index.html 

Commands: 

dirb http://10.1.1.14

    
Step 2: Log into phpmyadmin using root credentials and password pokemon.

Step 3: Look up exploit 3274

, 
Step 4: Use exploit to open a reverse shell into the database





## Examination Report – Remediation
### Patches and Updates 

Patch management can be a complex process. The importance of
each stage of the process, and the amount of time and resources
you should spend on it will depend on your organization's
infrastructure, requirements and overall security posture. Today
more and more companies rely on their information technology
infrastructure to enhance their business, save them money, and
increase their profitability. The threat of malicious virus and worm
attacks has been increasing, forcing businesses to reinvestigate
their security needs to better protect their environment. Combatting
these attacks has become a high priority. In response, vendors
produce security patches for their system vulnerabilities and make
them available to users.

Research has shown that the most efficient way to be protected
against attacks is to ensure that every machine in the environment
has the latest patches installed. If one system in the environment
is not patched, it can threaten the stability of the entire
environment and possibly inhibit normal functionality.

### Firewalls and Intrusion Prevention Systems
In today’s fast-changing IT world, even the best available security
is insufficient for the latest vulnerabilities in various products, and
against malware/attacks created to target those vulnerabilities.
While cyber-security cannot be 100 per cent fool-proof, we can still
try to achieve the maximum security possible. It is then, very
important to include firewalls and intrusion detection systems
(IDS)/intrusion protection systems (IPS), usually found in a
hardware-based offering that detect attackers and the
unauthorized access to a computer network and protect against
these attempted intrusions.

A firewall controls network traffic at the TCP/IP port level, by
blocking access to unwanted ports. However, it keeps open those
ports used by applications. Modern attackers are experts who
exploit software vulnerabilities by using technical tools, and devise
methods to break into a network to achieve their goals. To handle
smart attack attempts, an even smarter security mechanism is
needed, which will proactively and intelligently keep an eagle’s eye
on the network, and monitor and report incidents swiftly. IDSs or
IPSs are solutions that encompass these requirements.
Cyber security, like any other form of security, is a process of
continuous improvement. As more and more countries in the world
connect to the Internet, the resultant increase in awareness is
going to bring benefits, as well as its own set of problems.
Eventually IDS/IPS devices are going to be a de-facto standard
component in any IT infrastructure.

### Limit Unnecessary Services and Application Uptime

Running a network service on a device provides an avenue for
communications with other devices where one did not previously
exist. Any service may be subject to software flaws or poor
configurations that introduce security vulnerabilities leading to
compromise. Therefore, services unnecessary for the intended
purpose or operation of that device should be removed or disabled
to reduce the overall risk.

Most operating system vendors have now acknowledged the risk
of unnecessary services; therefore, generally more recent
operating systems are configured more securely by default.
However, all systems should be hardened.
Examples of how to harden systems that have been accepted as
industry standards can be found in several places. The Center for
Internet Security is one such place. They provide benchmarks for
your operating system for specific information about which
services can and should be disabled by default.
The Center for Internet Security web site is
https://www.cisecurity.org.

### User Permission Enforcement

From a technical level, role-based access control or RBAC is an
approach to restrict system access to authorized users. Put simply,
it means each user has a certain amount of data they can access,
depending on their role. By using role-based access, users only
have access to data and tasks deemed necessary to do what they
have to or need to.

There are several reasons to restrict user’s permissions on
systems.
• Social engineers like an easy target. If everybody has
access to all data, how easy is it for a social engineer to steal one
employee’s credentials and gain access to all the data? By limiting
access to data, you make the social engineer’s job harder and less
likely to target your business. Granted, a social engineer could find
a way to steal the credentials to someone who has the authorized
access to data, but with role based access, it would take more
work for them.
• One of the biggest ways hackers steal data is through non-
secured remote access software. It’s best to restrict those who
have remote access to only the data they can access. This will
help keep your data secure from hackers.
• The less people there are logging into your data, the less
openings hackers have into your environment. Restricting access
is just one way to make sure your data isn’t vulnerable to
attackers.
• By limiting access to users based on roles, it helps give
clarity to a user’s responsibilities. This will help your business
become more efficient in general. This way, you aren’t duplicating
or overlapping responsibilities. Confusion happens when user’s
roles aren’t clear. By using role-based access, you have to make
clear your user’s roles, what’s expected of them, and what
information they need access to.

### Script Blocking Programs

Because many web browser attacks require scripting, configuring
the browser to have scripting disabled by default reduces the
chances of exploitation. Blocking plug-in content, as well, helps to
mitigate any vulnerabilities in plug-in technologies, such as
JavaScript, Java, Flash and other plugins.

Browser vendors are now creating extensions for browsers that
allow execution of these types of scripts if the site hosting the
content is considered trusted by its user and has been previously
added to a whitelist.

Some of these extensions, like NoScript or NotScripts, also offer
additional countermeasures against certain well known security
exploits, such as Cross Site Scripting (XSS) and Clickjacking.

### Complex Password Utilization

No matter how many firewalls are placed around your systems,
there is always a key for complete access: your password. There
are many programs that attempt to steal passwords, by guessing
common ones, by randomly generating possibilities and trying
them all, “sniffing” it on the network or a combination of all these.
The best defense is a "strong password". A strong password is a
combination of numbers, uppercase letters, lowercase letters, and,
if possible, other characters. This makes the password nearly
impossible to guess in a reasonable amount of time, and ensures
that all the hard work you put into keeping your systems well-
defended does not go to waste. The longer the password, the
harder it is to guess.

As passwords get closer to random numbers and letters, they also
get harder to remember. That doesn't mean that you have to fall
back on a weaker password, though. You can m15peLL w0Rdz
intentionally, or use a mnemonic device like a strong passphrase.
Most systems also have built in ways to enforce the use of strong
passwords which will require the use of Upper and Lower case
letters, numbers and other characters as well as minimal length of
the password.

### Network Monitoring and Security Incident Event Management

Security information and event management (SIEM) is a group of
complex technologies that together, provide a centralized view into
an infrastructure. It provides analysis and workflow, correlation,
normalization, aggregation and reporting, as well as log
management.

Primarily, SIEM has been implemented in response to
governmental compliance requirements. Similarly, many
companies decide to implement SIEM in an effort to not only
protect sensitive data but also demonstrate proof that they’re doing
so, while meeting their compliance requirements.

A failed audit could have catastrophic results of loss of business
and employees, in addition to hefty fines. For these reason, many
companies regularly complete their own internal audit to validate
and verify that they are meeting these requirements.

### Logs 

The purpose of IT security is to be proactive and make it more
difficult for someone who attempts to compromise the network or
systems. To assist in these tasks you need to able to detect the
actual breaches as they are being attempted. This is where log
data helps.

To expose an attack or identify the damage caused, you need to
analyze the log events on your network in real-time. By collecting
and analyzing logs, you can understand what happens within your
network. Each log file contains many pieces of information that can
be invaluable, especially if you know how to read them and
analyze them. With proper analysis of this actionable data you can
identify intrusion attempts, misconfigured equipment, and many
more. Also for managing compliance, you need to retain logs and
review them.

When you know what is normal on your network, you can easily
spot what is abnormal by monitoring the log activity. It is very
critical to analyze the event to understand the root cause and to
make log analysis & log management more efficient, you need to
collect and consolidate log data across the environment, and
correlate events from multiple devices in real-time.
Also see the section on the importance of SIEM which correlates
with this information.

### Education

• Allocate and encourage continuing courses on security
• Connect with the local OWASP chapters
• Attend security conferences
• Network within the security community
• SANS courses
• Practice by creating your own vulnerable virtual lab
environments to test in
• Consider planning or requesting the employer to conduct
scheduled pen tests
• Conduct courses to strengthen and solidify your knowledge

### Vulnerability Scanning Tools

Vulnerability Scanners are automated tools that scan systems or
networks to look for potential points of exploit and identify security
holes. This category of tools is frequently referred to as Dynamic
Application Security Testing (DAST) Tools.

A vulnerability scan detects and classifies system weaknesses in
computers, networks and communications equipment and predicts
the effectiveness of countermeasures.

A vulnerability scanner runs from the end point of the person
inspecting the scan targets in question. The software compares
details about the target to a database of information about known
security holes in services and ports, anomalies in packet
construction, and potential paths to exploitable programs or
scripts. The scanner software attempts to exploit each vulnerability
that is discovered.

There are two approaches to vulnerability scanning, authenticated
and unauthenticated scans. In the unauthenticated method, the
tester performs the scan as an intruder would, without trusted
access to the network. Such a scan reveals vulnerabilities that can
be accessed without logging into the network. In an authenticated
scan, the tester logs in as a network user, revealing the
vulnerabilities that are accessible to a trusted user, or an intruder
that has gained access as a trusted user.
According to industry best practices, the best plan is to conduct
both types of scans.

### Recurring Penetration Tests

Penetration testing, also called pen testing, is the practice of
testing a computer system, network or Web application to find
vulnerabilities that an attacker could exploit.

Pen tests can be automated with software applications or they can
be performed manually. Either way, the process includes gathering
information about the target before the test (reconnaissance),
identifying possible entry points, attempting to break in (either
virtually or for real) and reporting back the findings.

The main objective of penetration testing is to determine security
weaknesses. A pen test can also be used to test an organization's
security policy compliance, its employees' security awareness and
the organization's ability to identify and respond to security
incidents.

With cyber-attacks becoming the norm, it is more important than
ever before to perform regular penetration testing to identify
vulnerabilities and ensure on a regular basis that the cyber
controls are working.






