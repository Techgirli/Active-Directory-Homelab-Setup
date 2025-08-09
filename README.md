# Active-Directory-Homelab-Setup
# Introduction
This document outlines the step-by-step process I used to create an Active Directory in VirtualBox. The lab simulates a small corporate network for IT administration, Soc Analysis and Cybersecurity.
# Lab Overview
The Lab consists of:
1)   Windows Server 2022 (Domain Controller + DNS + DHCP)
2)   Windows 10 (Domain Joined Client Machine)
3)   Kali Linux (For attacks)
4)   Ubuntu Server (Monitoring & Logging Server. I used Splunk, Elastic, and Wazuh occasionally)
5)   Virtual Box Networking ( NAT for internet access & Host Network)
6)   VirtualBox (virtualiztion)
7)   Sysmon (For Detection and Response rules)
8)   Splunk/Wazuh/ELK (SIEM /LOG ANALYSIS)
9)   BloodHound/Mimikatz/Metasploit and other attack simulation

# Tools & Technologies 
* VirtualBox
* Kali Linux
* Windows Server 2022 iso file
* Windows 10 iso file
* Ubuntu Server
* Active Directory Domain Services (ADDS)
# Goal
- It is to simulate real world Windows Domain environment to practice
- Active Directory Configuration
- Common attack techniques
- Detection & Defence strategies.
# Step-by-Step Setup
## Step 1:
The first thing i did was download the tools I would need for the AD
* Downloaded VirtualBox from the website:  https://www.virtualbox.org/
* Downloaded windows server 2022 iso file from the website: https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2022
* Downloaded Windows 10 iso file: https://www.microsoft.com/en-us/software-download/windows10
* Downloaded Kali Linux: https://www.kali.org/get-kali/#kali-installer-images
* Downloaded Ubuntu iso for VirtualBox: https://ubuntu.com/download/desktop
* Downloaded Sysmon on Windows : https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon
# Step 2: Setting Up the Virtual Network
* I created an Internal-only Virtual network in VirtualBox
* I named it Host-Only Adapter
* I assigned static IPs mannually to each (Windows server, Windows 10, Ubuntu Server, and Kali Linux) it doesn't connect to the internet.
# Step 3: Building the Domain Controller
* I installed Windows Server 2022, assigned static IPs (162.168.56.**), changed the Hostname was Hostname Manager.
* Installed Active Directory Domain Controller, I used the Server Manger to Add Roles and Features, I chose Active Directory Domain Services.
* I promoted it to the Domain Controller, created new Forest and named it Conti.Local.
* I created Users to simulate an organization with different departments like IT, Finance and HR. Examples {Ciara,Tim,Luke}
# Step 4: Setting Up the Domain-Joined Windows
* I installed Windows 10, I assigned static IP 192.168.56.**, I used the internal network
* I joined the Domain, join Conti.Local
* I installed Sysmon and used the sysmon config
* Enabled Windows Event Forwarding (WEF), configure subscriptions and forward logs to the SIEM.
# Step 5: Setting up Kali Linux (Attacker)
* I installed Kali Linux in VitualBox
* Then I assigned a static Ip address and connected it to the Hostname Manager
* I updated and upgradeed the Kali Linux using: sudo apt-get update && sudo apt-get upgrade
* I installed the necessary tools for the attacks
# Step 6: Setting up Ubuntu Linux
* I installed ubuntu linux iso and also updated and upgraded it
* I assigned a static IP address
* I installed Splunk and Elastic on my Ubuntu server
# Step 7: Pinging all the virtual machines to make sure they are in communation.
* I pinged each of the virtual machines to eachother to make sure they are in communication
* It was a success.
# Step 8: Lessons Learnt from this
I faced some challenges in networking, I had to create both a NAT connection which was for internet connection, and a static connection to just the Virtual machine which was to help with downloads and updates, when it is time to do some attack i would disconnect the NAT (internet connection) and connect only to virtual host IP address alone.
I was able to do some research, watch videos and it helped with my hands on experience and learning.
