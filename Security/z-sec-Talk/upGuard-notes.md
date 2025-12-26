UpGuard Blog 11 strategies to have the highest chances of preventing supply chain attacks.

1. Implement Honeytokens
Honeytokens are decoy resources that act like tripwires when a cybercriminal attempts to access it. 

2. Secure Privileged Access Management
- Educate staff - they are primary gateways
- Manage many access accounts from a single interface 
- Encrypt all internal data
- Protect processes and technologies (antivirus, mfa, attack-surface monitors)  

3. Assume all network activity is malicious by default (Zero Trust Architecture). A request can access intellectual property only after passing a strict list of policies. 

4. Assume you will suffer a data breach (mind-set)

5. Identify all potential insider threats that arise from mis-education and an unsupportive work culture 

6. Identify and protect vulnerable resources (via honeytokens)

7. Identify and Minimize access to sensitive data

8. Restrict use of non/approved IT devices

9. Regularly assess third-party vulnerabilities  

Organizations have a 27.7% chance of suffering a data breach, and almost 60% of these breaches are linked to third-parties.


An outlying computer or network of computers 
malware pings it
mimics normal web traffic 
C2 replies with info about other essential domains + extra instructions / payloads


1.  Attacker accesses ADFS server and extracts private key and certificate.

2.   User attempts to access desired service (e.g. AWS, Office 365).

3.   Service redirects attacker to ADFS for authentication.

4.   Bypassing ADFS authentication, attacker signs a forged SAML response with stolen key.

5.   Attacker presents desired service with signed SAML response and receives access.


1.  User attempts to access desired service (e.g. AWS, Office 365).

2.  Service redirects user to ADFS for authentication.

3.  User authenticates with ADFS according to Domain policy (e.g. Multi-Factor-Authentication).

4.  ADFS returns signed SAML response to user machine.

5.  User presents desired service with signed SAML response and receives access.


