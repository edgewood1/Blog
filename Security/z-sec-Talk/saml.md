Is this cloud or on-premise? 

- steal SAML signing keys 
- gain admin privileges

- forge web credentials by escalating AD privileges in order to compromise signing certificate


- initial objective to collect info on vicitms enviroment - done via certificate THEN create tokens and present them to services that trust saml tokens. 

- since hackers appear legitimate, theres not fix.  
 


OR LDAP enumeration to get admin priv.

aka GOLDEN SAML ATTACK: forging a saml auth object. they can then pick what user and privlieges they desire.





https://www.microsoft.com/security/blog/2020/12/18/analyzing-solorigate-the-compromised-dll-file-that-started-a-sophisticated-cyberattack-and-how-microsoft-defender-helps-protect/

 
* good image : honing in: golden saml attack


AZURE AD
- cloud based identity and access management service
- It can act as an Identity provider for the various services (apps) on a network.  
- Admins can use it control access to apps / resources, eg. require multi-factor auth.
- Developers use it as a standard for adding single sign-on, allowing it wor wwork with users pre-existing credentials. 


- change AAD settings to make this easier.

Attack
- They still don’t know how the actor gained access to the certificates. 
- used stolen passwords? to access privlieged account 
- golden saml attack to access compromised certificate
- The SAML federation server database can be accessed remotely 
- They may have stolen tokens aout of memory.
- Mimikatz, which has been used to hijack Azure accounts.  
- It could be that users had broad access to the cloud environment - with permissions to setup SSO enabled apps that generated valid tokens. 
- https://medium.com/cloud-security/solarwinds-hack-retrospective-322f03b4eb9b
