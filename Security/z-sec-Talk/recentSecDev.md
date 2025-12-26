Overall 
1. 5 W’s 
2. Attack Summary
3. Discovery
4. Prevention
 
5 W'S
=====
- who: russians / americans
- where: solarwinds / orion
- why: intelligence gathering
- when: began 2020 / spread march - june 2021 / exposed recently
- WHAT: Malware v virus v worms v trojans < delivery mech
  = their actions > backdoor, ransomware
- dark time? 

HOW DID IT HAPPEN? 
=============
PRIOR TO ATTACK
Recon: gather info about target org 
Resource Development: setup command and control infrastructure

MITRE website
=========

ATTACK SUMMARY
=======
- ACCESS /EXECUTION (part 1 + 2)
- DISCOVERY / COLLECTION
- COMMAND CONTROL / EXFILTRATION

ACCESS EXECUTE: PART 2 
======
- Supply chain Compromise: product manipulated prior to receipt by a final consumer 
- Type:  a “trojan” malware, "trojanized" update.
- The update goes out to 18K customers over a period of 3 months.   
- After update activated,  malware stays dormant / invisible for up to two weeks. 

EXECUTION pt 2: 
======
When app starts, DLL loads and runs backdoor code that begins "ON-GOING PHASE"

- waits 2 weeks then checks that coast is clear

Discovery: trying to figure out your environment, i.e., exploring what they can control
- inspects environment: am I in the right place?
Persistence: trying to maintain their foothold, i.e., changing configurations; valid accounts
- persistence: if so, how do I stay alive?

Collection: gathering data of interest to the adversary goal, i.e., accessing data in cloud storage / DATA FRom local system
- collection: and gathers info from local system?
Obfuscation - the act of making it hard to see commands executed or making its files look benign.
Defense Evasion: trying to avoid being detected, i.e., using trusted processes to hide malware; Environmental keying, disable / modifying tools, 
- defense evasion: and stay hidden?
    - environmental keying, disable / modify tools (impair defenses)
- only ever ran when it did not detect anti-virus / forensic tools
- it mimicked Orion network protocols,  
- Malware changes subdomain each time it sends traffic, using a domain generation algo, 
- Communications with C2 was limited to 1-minute for any one IP / subdomain, making it harder to id on a log 
- Logs relating to its own activity were excluded or altered.   
... 

Lateral Movement: moving through your environment, i.e., using legitimate credentials to pivot through multiple systems
------
 

FURTHER ACCESS
==========
Privilege Escalation: trying to gain higher-level permissions, i.e., leveraging a vulnerability to elevate access
Credential Access: stealing accounts names and passwords, i.e., keylogging
Exfiltration: stealing data, i.e., transfer data to cloud account
Impact: manipulate, interrupt, or destroy systems and data, i.e., encrypting data with ransomware

extra terms
- lsdap enumeration, 
- DSSync attack, 
- ADFSserver accessed, 
- stolen SMAML signing key


DCSync 
- an attack where attacker impersonates a domain controller and request password hashes from other DCs
- simultaes the behavior of Domain Controller (DC) in order to retrieve password data via domain replication. 
- Once an attacker has access to a privileged account with domain replication rights, the attacker can utilize replication protocols to mimic a domain controller. 
 
LDAP (Lightweight Directory Access Protocol)
- a protocol used to access directory listings within Active Directory or from other Directory Services.  
- tied to DNS to allow lookups 
-  It is possible to query the LDAP service, sometimes anonymously to determine a great deal of information that could glean the tester, valid usernames, addresses, departmental details that could be utilised in a brute force or social engineering attack.









PREVENTION: DEVOPS 

PREVENTION: SUPPLY CHAIN

- Third party apps 

PREVENTION: ADD / SAML






DEVOPS
How to secure devops pipeline?  “DevSecOps,” 
- automated vulnerability scanning and other tools
  
xxx


========
timeline
=======
inappropriately secured administrative credentials accessible via external remote access services

rdp - remote desktop protoacl - a remote desktop solution in pcs

if network not well secured, then it can be accessed 
out of date versions of rdp
used to steal a sysadmin password
they can use 

before 10-19
Solarwinds infrastructure breached

- took advantage of known Microsoft configuration issues to get email / docs stored on cloud.
- third party apps? 
- a comprmised solarwinds email account> gain access to and exploit our Orion development environment.for the SolarWinds Orion network monitoring platform




10-19 - software modification testing
- The hackers then spent months implementing botnet command-and-control protocols, 
-modified their first files
- no malicious backdoor code, but it indicates that this is when the attackers first started making 
- tests for modifying the software. 


The build system was then used to create a malicious software patch that SolarWinds says it shipped out to fewer than 18,000 customers in 2020.


 
 =====
 sunspot - used to insert the sunburst backdoor into software builds.  a build implant. deployed into the build env to inject the backdoor.   
 sunburst - the malware that creates backdoor in the updates

C2 infrastructure is built with the intent to pursue several goals:
hide the true location of the C2 server;
mimic legitimate communication;
allow only malware control traffic to reach the real C2 server;
be reliable — given detection the part of C2 infrastructure, still, maintain C2 channel to the target.

https://ditrizna.medium.com/design-and-setup-of-c2-traffic-redirectors-ec3c11bd227d


- was the version control system was compromised or the trojanized software was placed directly on the build machine.
- While it's not immediately clear how the attackers got access to the code base,  
- SolarWinds' update server being accessible with the password "solarwinds123" assumes new significance given the overlap in timelines.

CONCLUSION

"Hiding in plain sight behind a globally known software brand or a trusted business-critical process, gives this method access that a phishing campaign could only dream to achieve," he added.


HOSPITALS
===========

- Trickbot malware attacked more than 400 hospitals in the U.S.
- it frequently works with ransomware operators Ryuk 
- claimed to have ransomed about 30 medical facilities around the country

prymts.com: 
- A national survey has found more than 80 percent of medical practices have been the victims of cyberattacks, 
- More than half of the hospital and medical facilities reported patient safety concerns from the data breaches,
- 20 percent said that their business had been interrupted for more than five hours, the survey said, according to USA Today.
- IBM reported there was a 6,000 percent increase in spam attacks on IT systems from March through April as the pandemic unfolded, many of them at healthcare facilities.
- For example, the amount of attempted hacking doubled in March at Seattle Children's Hospital. The attacks came in the form of phishing emails, seeking a staffer who would click on a malicious link and allow malware into the health system's network.
- In 2014, the FBI reported a stolen credit card or a Social Security number was worth just $1 on the black market, while an electronic health record would fetch up to $1,000 if it belonged to a well-known person, USA Today reported.
- health records can also be used to file fraudulent insurance claims and obtain prescription drugs.

 
Verge
- Health records, test results, and prescriptions are stored in the cloud and are susceptible to hackers. 
- a blood-testing companies was hacked via their billing collections vendor, and the financial and medical records for more than 12 million patients were exposed. 
- Another risk is that medical information can be intercepted, hijacked, and in worse case scenarios, altered in ways that can lead to misdiagnosis and incorrect treatment plans.

https://www.theverge.com/2019/4/4/18293817/cybersecurity-hospitals-health-care-scan-simulation

=====

Malware classified by type: 

