
The underlying problem when you see this error is that the machine you are trying to access can no longer communicate securely with the Active Directory domain to which it is joined. The machine’s private secret is not set to the same value store in the domain controller. You can think of this secret as a password but really it’s some bits of cryptographic data called a Kerberos keytab stored in the local security authority. When you try to access this machine using a domain account, it fails to verify the Kerberos ticket you receive from Active Directory against the private secret that it stores locally. I think you can also come across this error if for some reason the system time on the machine is out of sync with the system time on the domain controller. This solution also fixes that problem.

##The standard fix This problem can be caused by various circumstances, but I most commonly run into it when I reset a virtual machine to a system snapshot that I made months or even years before. When the machine is reset, it is missing all of the automatic password changes that it executed against the domain controller during the intervening months. The password changes are required to maintain the security integrity of the domain.


Domain
Domain name - www.molly.com
Molly - second level domain
.com - top level domain (tld) / domain extensions
Www - subdomain / an extension of a domain name, working as a separate web address, or specific ip addresses or directories - sets it appart from the main site - it has its own address without having to register a new address site.   Replace “www” with “store - store.molly.com or news.mollly.com // subset of a registered domain name
Subdomain - a domain that is part of another domain.  
DNS resolution means translating IP address to domain name.  A ip address looked up, call made to dns server for network to resolve dns entries.  
