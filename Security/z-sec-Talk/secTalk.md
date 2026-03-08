
prevention





distribution of malware? 

growth of malware? 



A backdoor attack is a type of malware that gives cybercriminals unauthorized access to a website. Cybercriminals install the malware through unsecured points of entry, such as outdated plug-ins or input fields. Once they enter through the back door, they have access to all your company’s data, including customers’ personal identifiable information (PII).

Small and midsize businesses are particularly vulnerable to backdoor attacks because they tend to have fewer resources to close off entry points or identify successful attacks. Cybercriminals know that SMBs often lack the budget or security experts to prevent and mitigate attacks. That’s likely why 43% of cyberattacks are aimed at small businesses.

Malware puts the backdoor in place
backdoor is a type of malware
it is a method of bypassing authentication / encription

Backdoors are most often used for securing remote access to a computer, or obtaining access to plaintext in cryptographic systems. From there it may be used to gain access to privileged information like passwords, corrupt or delete data on hard drives, or transfer information within autoschediastic networks.

deliberate backdoors give an owner a way of restoring passwords

 
=====
exploit - a piece of software or chunk of data, that takes advantage of a bug or vulnterability, leading to privliege escallation, or a ddenail of service attack. 

vulnerability - a weakness in a system - a tool addresses this weakness.  v's also called attack serface.  (input validation, clickjacking, race conditions, privliege escaltion, )
it exploited unpatched computers.  
 
>>it infects cpu . looks in network to find other devices available and suspectible to vulnerability, it uses an exploit called eternalblue, it installs it, which installs backdoor and downloads worm, repeat.  

spyware - gathers log keystrokes
 

 

 

diffrence spyware / trojan

rootkit - modifie s core system files - kernel - not an app in the os, it becomes part of the os, now it has complete control of os, won't see it in task manager - invisible to anti-virus - rare - 

 

scrip virus - browser based
macro - common in offic


all damange

how people interact? 
how they spread?
self-contained / part of program

virus - propagates a copy of itself to another program - attach to good files or be self-contained and search out other... attached on an exe file - won't spread until user runs it - when host code exe so it viral code.  transfer doc, the worm virus spread.

worm - replicate copies of themselves; standalone software, don't require humna; exploit vulnerable or social engineering, leverage ransomwware 


glossary 

malware (wiki) 

single signon - an auth scheme that allows a single ID / pw for accessing several related yet independent software systems.  you log in once ancd access services without re-entering authen factors.  

differnt from same-sign on  

public key certificate = digital / identity certificate - an electron doc that proves ownership of public key and signature of entity that verified the certs content - used to communicate securely... 

certificate authority is the issuer - charges customer to issue cert - 

web of trust scheme - people sign each others ... first one is the public-key shceme. 

SAML - 

TIMELINE

MALWARE attacks rising

reduce
https://www.digitalocean.com/community/tutorials/js-finally-understand-reduce

test1

articles

https://www.wired.com/story/macos-malware-shlayer-gatekeeper-notarization/?utm_brand=wired&utm_campaign=cm&utm_mailing=WIR_SubPersRec_2_02012020&utm_medium=email&utm_source=crm&utm_term=WIR_PersRec_Freq_Test_2021-04-28_C

https://www.healthcareitnews.com/node/537411

Dos, flooder, virTool, HackTool, Constructor, Spoofer
these find an exploit
leads to a rootkit to introduce a trojantrojan-spy, trojan, sms, trojan-proxy
this opens backdoor to virus / worm 


deny service, spread, stela, ... 
by usermode, kernal mode, hypervisor, hardware -- various rings - by piv. 






=====

active directory - way of managing a network

peer - peer = all networks equal
no server in overall computer
each has its own local security db - passwords, etc
used in small organization.
10 users is suggested limti

client-server network


server
- directory service (server) - central security database with all the users, passwords, and permisssions.  
- mel logs on, server verifies her credentials, if correct, she gets into her computer. 
- in ms server network, active directory is the tech that gives us a centrally managed network.
- ad is a suite of services

- domain services (just ad)** - the heart that binds the other features
- certificate services
- federation services
- rights management services
- light weight directory services


ADDS - > server is a domain controller
- hosts AD's domain db - stores users, groups, computers, 
- 

Domain > trust > child domains = forest (container of all AD objects)

domains- admin unit that contains cmputers, users, grups
many domains - a forest
trust enable users in one domain to access resources in another

ittaster
https://www.youtube.com/watch?v=pmMxT9YKzTE

===
dns
==
domain name system

computers are on networks
ip addresses - identify each computer
dns translates ipaddress to names

www.example.com
- is the ip in the cashe?
- os asks a resolving name server > asks very servers

regsitrar - assigns servers and domain
registry - has info


domain - a group of files / users
domain name - www.yahoo.com
ip address - location of domain


1. setup server - gives you an ipaddress
2. buy a domain name 
3. in name cheap: 
nameservers > write down the 3 names
gives do permission to do with it.  

in digital ocean (do first)
point ip address to domain name
create > domain/dns
type in domain name > add domain
add hostname: ip address for project
www.xyz.com
xyz.com > both point to ipaddress

---
go to django project > settings.py > add domain name to allowed hosts

alter gunicorn

---

domain - a collection of objects on a netwrok - computers, users, etc

controller - governs domain functions like authorization and acccess

ad - controller // other controllers create domain

in controller, you say: i want no one to do X
- a software with a function
- authnetication server
-add all computers to ad list of acceptable users
- these computers are part of the domain
- if cpu is part of doamin, when i go to my cpu, i see a login screen, type in username and pw, that's sent to domain controller, looks this up, if correct, it'll check what you have permissions to see and what security policy to have, bubbles that into a key sent back to computer so it can read it and see what I can access on the network / domain. 

users

