

admin/settings

security settings

Use Security Splash Disclaimer	 No  Yes	

how to turn this off - what's thie

default settings not turning this off

testapi - he did commit to master 
is matt executing test api thru script?
is it updating the test api - did he update the version number.


maven pro 28

cc
An outlying computer or network of computers
- malware pings it
- mimics normal web traffic 
- c2 replies with info about other essential domains + extra instructions / payloads 



2/20

- they started setup of C2 domains 

 
Surprise - Over the past several years, the US has invested billions of dollars in Einstein, a system designed to detect digital intrusions. But because the SolarWinds hack was what's known as a "supply chain" attack, in which Russia compromised a trusted tool rather than using known malware to break in, Einstein failed spectacularly
- SUNSPOT
- executes 

====
-SUNBURST
- malcode inserted
- client downloads software
- DLL loads + malcode invoked on boot
- DEFENSE EVASION/RECON: backdoor runs checks; if any fail, it shuts down: 
  - is it running running in a n actual compromised network?
  - has it been 2 weeks?
  - is security-related software running?
  - it checks other conditions via domain / edpoint checks?
  EXECUTES
- RECON: it gathers info
- INITIAL C2 - 
  - it connects with predefined c2 to report basic info + get first commands
  - it creates a unique subdomain that identifies device, so each compromised device will call a different subdomain
  - see figure 6
  - first part a hash of network address, device domain, and registry value from a key
  - generates a pseudo-random URI that is requested on the C2 domain
  - hxxps://3mu76044hgf7shjf[.]appsync-api[.]eu-west-1[.]avsvmcloud[.]com /swip/upd/Orion[.]Wireless[.]xml
  - backdoor composes a JSON document into which it adds the unique user ID described earlier, a session ID, and a set of other non-relevant data fields. It then sends this JSON document to the C2 server.
  - If the communication is successful, the C2 responds with an encoded, compressed buffer of data containing commands for the backdoor to execute. The C2 might also respond with information about an additional C2 address to report to. 
  - In a nutshell, these commands allow the attackers to run, stop, and enumerate processes; read, write, and enumerate files and registry keys; collect and upload information about the device; and restart the device, wait, or exit. The command CollectSystemDescription retrieves the following information:

Local Computer Domain name
Administrator Account SID
HostName
Username
OS Version
System Directory
Device uptime
Information about the network interfaces

- EXFILTRATION - send info to attacker.
- run command received from cattacker.  
- KEYBOARD ATTACK
- once backdoor is 
- attacker begins other activitings credential theft, escalate privliege, and lateral movement
- Once backdoor access is obtained, the attackers follow the standard playbook of privilege escalation exploration, credential theft, and lateral movement hunting for high-value accounts and assets. To avoid detection, attackers renamed Windows administrative tools like adfind.exe which were then used for domain enumeration.
====
 

======

FROM INITIAL C2 IF YOU SHOW A PHOTO

  - first part a hash of network address, device domain, and registry value from a key
- URI: hxxps://3mu76044hgf7shjf[.]appsync-api[.]eu-west-1[.]avsvmcloud[.]com /swip/upd/Orion[.]Wireless[.]xml


AFTER EFFECTS

Mar - Jun - malware on software downloaded .
Months after - SVR had access to networks to further exploit, covering tracks so they are hard to detect / remove, thus, gaining “persistent access”.  Although uncovered, this access could be the staging for larger attacks.
It will take years to know for certain which networks the Russians control and which ones they just occupy.Its hard to get this off the networks.  Requires replacing whole networks while keeping them operational.  Essentially, a “do over” - rebuilt networks in isolation from compromised networks. 