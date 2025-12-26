Authnetication

a list of common weaknesses / o

https://cwe.mitre.org/data/definitions/287.html


 
https://www.khanacademy.org/computing/computers-and-internet/xcae6f4a7ff015e7d:the-internet/xcae6f4a7ff015e7d:the-internet-protocol-suite/a/the-internet-protocols

HISTORY 

Vannevar Bush, an electrical engineer at MIT wrote an Atlantic Monthly article in 1945 (As we may think” where he said that the amount of scholarly articles were accumulating faster than we could read them.  So he imagined a system  where it would all be sored on microfilm for quick consultation.  Via contextual associations with related topics much in “the way the mind links dta together”.   This was a memex system
Ted Nelson coined Htypertext in 193 to mean a body of written or pictorial material interconnected in such a complex way that it could not ocnveniently be presented on paper.  A true “docuverse”.  In 1970s he created Xanandu, a prototype hypertext system.
1989: HTTP is born at CERN.  Tim Berners-Lee proposed a system for tracking the info created by the soon to exist large hadron collider.  He imagined it as “human-readable info linked together in an unconstrained way” (his definition of hypertext) and hypermedia - “a term that indicates “one is not bound to a text”.
HTTP/0.9 - has one method (GET) to only fetch text.  
96- HTTP/1.0 - spec grew from 1 - 60pgs.  Response codes, errors, redirects, more methods.  
99 - 1.1 - patch.  No longer needs to reestablish connection after each request.  
15 - 2.0 - huge departure.  

 TCP invented 1974 / 78- tcp3 split into tcp/ip,  in 82 it was teh standard in defense industry. 89- ip suite spec complete

- http .9 0 1991
- inth http/1 / 96 - connection closed after a single request/response pair.
- 1.1 / 97 - a keep-alive-mechanism introduced - allowed multy requests. 
- persistent connectiosn reduce request latenncy b/c client doesn't need to re-negotiate the TCP 3-way-handshake after first request.  
- latency - time delay between cause and effect.  the lag.  time interval between input to a stimulation and the visual response, often result of network delay. 
- 1.1 - chunk transfer encoding to allow content on persistent connections to be streamed rather than buffered. 
- http pipelining - allows multiple requests before waiting for each response.  
- http is stateless protocol, so http server doesn't keep info about each request.  - but we use states / server side sessions usn gcookies, etc
- http provides two authentication schemes where server asks identity 
  - basic access
  - digest access 

95 - SSL  - enabled companies to handle credit card tranactions online and helping prove that merchangets you visited were who they said they were. 
this stayed in credit card ciricles - they didn't see why we should encrypt everything. 
then unencrypted passwords wreer being stolen
2011 - ssl2 deprecated - due to security vulnerabilities
2015 - ssl3 deprecated - 
1999 - TLS updgraded ssl3 - additional protections
2006 tls 1.1
tls 1.2 2008
tls 1.3 - 2018(10 years and 28 drafts to complete).  

tls / ssl are cryptgraphic security protocols that provide dta integrity / privacy.  they allow connection between two to be encrypted so third parties can't read.  it's human readalbe without it.  a cookie is visible in plain text. 

https://www.acunetix.com/blog/articles/history-of-tls-ssl-part-2/

HTTP TRANSACTION 1

 1. I enter /amazon.com
 2. Server responsds with login page / certificate w/ public key


CERTIFICATE

What is a certificate? 

tls / security / digital certificates 
- guaratees website identity via trusted third party 
- data is secure 

Anyone can create a certificate claiming to be whatever website they want.

What does it look like? 

HTTP TRANSACTION 2 

I encrypt my data with their public key and send my public key + password + username. 

ENCRYPTION 

how does encryption work? 

using a salt can preven tthis
salt is random dta added to encryption process. 

to use tls: 
- get tls certificate issued by a certificate authoerity th.  
- it states who onwns teh domain, teh server's public key.  
- this validates servers identity.

on arriving to website
- get cert
- what version of tls to use
-  which cipher suites (set of algorhythims) to encrypt? 
  
terms - 

cryptography - change plaintext to cipher (encrypted) text

encryption uses a alorhthims: aes, rsa, des

kinds of criptography (encryption)

hashing - - not used to hide msg bu t to verify the contnets - 

key - info used for scramling data so it apppears random; a large number string of letters, 

symmetric cryptography- uses the same kkey to encrypt and decrypt / one key to open and close a trunk where both people have a key. 

asymetric - uses two keys - public / private: this makes https possible

1. encrypt with public must be decripted with private
2. encrypt with private must be ... 


 assymetirc process

- lock has 3 states: locked-key-left, unloked, and lockedkey-right
- 2 keys - one goes right (A can open ) other goes left.
- so rightkey locks, only left key can unlock; vv
- either key can lock, but only the opposing key can open
- bob shares left-turn key, keeps right-turn for self
- now alice can send bob secret stuff locked with left-turn key, knowing only bob can unlock
- bob can send alice stuff locked with right-turn key, and only she can open it - also she knows its from bob because her key opens it. 


 https://www.cloudflare.com/learning/ssl/how-does-public-key-encryption-work/

HTTP TRANSACTION 3 

they decrypt with their private key, etc

MULTI-AUTH 

Here, we only needed a password / username to enter.

But we can use multiple forms of authentication: multi-auth

Multi-factor - we present two or more pieces of evidence (or factors) to an authentication mechanism: 
- knowledge (something the user and only the user knows), 
- possession (something the user and only the user has), 
- inherence (something the user and only the user is).  

What we use:  A third-party authenticator (TPA) app enables two-factor authentication, usually by showing a randomly-generated and constantly refreshing code which the user can use.


HTTP TRANSACTION 4 -  

when cleared we begin exchange / accessing data 

cipher algorhitims cipher the rest of teh data. 
Cipher - alogorithm that can encode cleartext to make it unreadable and deecod it back.  

symmetric-key cryptography

public-key cryptography

https://pragmaticwebsecurity.com/articles/oauthoidc/refresh-token-protection-implications.html

SESSION BEGINS




WHAT IS A WEAK AUTH MECHANISM? 

Weak Authentication describes any scenario where we have high value assets protected by a low strength barrier, allowing for easy unauthorized access



prevention

* always look at domain name. 
* used good passwords. 

prevention


 
imporper cert validation... 
https://cwe.mitre.org/data/definitions/287.html




 

SESSOIN MANAGEMENT 

Scenario #3: Application session timeouts aren’t set properly. A user uses a public computer to access an application. Instead of selecting “logout” the user simply closes the browser tab and walks away. An attacker uses the same browser an hour later, and the user is still authenticated.




Multi-factor authentication (MFA) - considered best defense against password-related attacks.  Microsoft suggesting that it would have stopped 99.9% of account compromises.  Not ideal in all circumstances 

It coudld be use in suspect scenerios:  

A new browser/device or IP address.
An unusual country or location.
Specific countries that are considered untrusted.
An IP address that appears on known blacklists.
An IP address that has tried to login to multiple accounts.
A login attempt that appears to be scripted rather than manual.
Additionally, for enterprise applications, known trusted IP ranges could be added to a whitelist so that MFA is not required when users connect from these ranges.



session id === access token // ? 

__session management__

WHAT IS A SESSION? 

- user-app interactions that occur within a given time frame.  lasts until theres 30 min of inactivity.  Can be redefined to suit a company's agenda. 
- it begins on login, after server sends tokens - usually a string with encoded data about user, session, etc. 

          TOKEN BASED - no session persists server-side - stateless.   token string has info abou tuser, roles, etc.  tokens are created using a hash mechanism, symetrical encryption (AES), assymetrical encryption (RSA). 

          alternative - SESSION-BASED - a session id issued.  its just a string - an identifier.  the server must do everything else - look up user, finder its roles, get its data.  scales poorly.  requires lots of memory. 
          SessionID - a long, unique, random string. By itself there is no user information. When server receives a SessionID, it needs to do extra work to find out which user it belongs to, and then what s/he can do. This extra work often requires a database lookup.


          MOST COMMON TOKEN 
          
          jwt - holds metadata, it can self-expire so nothing to hold in database? 

          SON Web Token (JWT)  
          - JSON object
          - a compact and self-contained way for securely transmitting information.  
          - This information can be verified and trusted because it is digitally signed. 
          - JWTs can be signed using a secret (with the HMAC algorithm) or a public/private key pair using RSA or ECDSA.
          - it is readable: https://jwt.io/
          - A JWT contains three parts: <header, payload, signature>. 
          payload contains who the user is and what s/he can do, and signature verifies the token is valid.  
          - alterantives: paseto, branca, macaroons 
          - it passes it via http header ===>> authorization: bearer JWT
          - if not sent via https or oauth, it can be stolen.  

 
- after login, an access token + refresh token given 
  
access 
- sent with request header called auhorization.  This is a bearer token. 
- allows direct resource access
- server uses token to decide whether the client is authorized or not. 
- have an expiration date and are short-lived.

Refresh 
Refresh tokens: A token used to obtain a renewed access token without having to re-authenticate the user.

- allows us to get a new access token from the authentication server
- ie, old token expires, so we use refresh to get a new one.
- we don't have a token at all, so we use refresh to get a new one
- also expire but are rather long-lived. Refresh tokens are usually 
- subject to strict storage requirements to ensure they are not leaked. 
- can also be blacklisted by the authorization server.

Advantage of two tokens:
 
- Improved access patterns against the authorization server (lower load, faster checks)
- Shorter windows of access for leaked access tokens (these expire quickly, reducing the chance of a leaked token allowing access to a protected resource)

- one endpoint issues all tokens
- teh rest of teh endpoints checks for access token

https://auth0.com/blog/refresh-tokens-what-are-they-and-when-to-use-them/

LOGIN PROCESS REVISED

- login in to amazon / access + refresh tokens sent
- access token expires after 20 minutes of no action
- to continue you need refresh token or new auth round
- when you return, you're browser will send the refresh token instead (rather than the password / new login).
- if this is non-existent or expired, then a new auth round required. 

Sliding expiration means that each time the session is accessed it will reset the timer back to 20 minutes again.  When sliding session expires, our tokens expire.

With each action, a new access token is issued OR the time on the access token reset.  When it expires, you'll need to use a refresh token to get a new access token OR a new auth round - depends on the requirements of the dev team. 

If someone steals a refresh token
- they can use it to get new access tokens. 
- access tokens can be blacklisted.  but it will eventually expire.

 
HOW WE USE IT:  

- we initially stored our tokens in local storage, but not anymore.
- we don't put it on the cookie
- we put it in the  header of the requests
- authorization: bearer >> 
- bearer is the kind of token it is -
  - as opposed to basic, digest... see spec on auth token
- in order to get studies, we need access token
- ssl encrypts requests between client and server - 
- they can monoitor network but- uses browser's encryption / to steal? 
- if cs on http then unecrypted anyone can monitor the traffic. 

ISSUES WITH SESSIONS 



END NOTES

 



Running a server
Need a server: nghttp2 package 
Need a TLS certificate.  

HTTP protocol (old school)
Stateless > each request hold no data about previous ones
So we should authenticate each time. 
Old school: cookies
Session-based auth makes it stateful - both server / client keep a record
Frontend: cookie holds session identifier passed with each request. 
Enter username / pw
Server checks user, returns unique token which is saved in its own memory
Client sotres token in cookies and sends it back with each request
Server authenticates user with token and returns request
Log out? Token is removed

Issues
With each auth, server creates a record of all their data. If many users are logging in at once / as more users - there’s a strain.

Example3: JWT-based auth (json web tokens)
User Info not stored on the server or in a session
User logs in
Server verifies creds, returns signed token w/metadata such as permissions
Token stored client side, local storage
Subsequent request to server include token in auth header in the form of a bearer or in post request
Server decode jwt - if valid, processes request
Token destroyed on logout

Benefits
Stateless
Metadata can be stored in a token
Single call to data vs. multiple: session valid? User role? Get data? 


Problems
Solutions
Session Management points


xxxxxxxx


1

What has been discussed? 


2

how to let app access user data without user giving password

enter password only in one place - at oauth

login in to twitter using google, you get sent to google where you submit password, then they come back with ok.
user sent away from app to oauth server, then they come back to app
keeps password safe...

google - type in password into accounts.google.com

Alan - 
Surface area
Vulnerability: Deserialization of untrusted data

Marcus- 
XXS attacks
CSRF

Vahid- 
csv injection
sql injection


vulnerability - a weakness in the application
attacks - strategies used by an attacker
controls - what a person could > 

controls that could be put into place? 

----

sql injection attack via improper data validation vulnerability
code injection attack via 

thoroughly explain the attack / vulnerability so it's clear to the team
provide concreete rather than abstact examples. 
my findings from my research. 


my main exporsure through code. 
so for this presentation
i spent most of my time pouring over basic definitions / images
towards then end, articles 
lots of links - for my future reference

topics covered could be unfolded - deeper diver - later. 
- if anyone has extra info on any point, please jump in, share, correct, educate. 

3

auth - what is it? 
what happens when we submit a name into the url? https AND what are the vulnerabiliteis
- 2nd thing 
3d

2

objects / workflows I'd come acrros while devleoping
such as making sure tokens... 

But beyond these, I couldn't say much more
What kind of token was this? 
where'd it come from? 
etc? 

1
meanders off track on occassion
take liberties with 
2

attacks and vulnerabilites associated with auth / sessions. 

3- 
broken down into 4 sections

vulnerabiliteis associated with https / certificates

4
a few of the risks have shifted / merged 

5 

broken auth - this process isn't handled well
and leads to stolen passwords. 

straight from mdn - 

change to first person

6 list history



9

creating an encryped connection is called a "handshake"
it consists of 3 steps

algorhitims my browser could use 

pick one of the cipher suites my browser has offered

we both have secret, two strings
combine these to create a session key
we use this to encrypt/ decrypt

10

when you arrive at a website 
padlock next to the address implies the certificatesclick on this - for details

open certificate - for details.  

11

most browsers are willing to truest 150-250 root certificates  representing 52-101 organizations


https vulnerabiliteisq move to before certificates


cert trans is an organization that checks for... 


Back to our login page. 

controls.. 

18

why are complex passwords important? 

They pose a greater challenge to hash cracking methods. 

where 
1. hashed password stolen
2. compared against a list of known hashes
- list of likely candidates
- lists of every possible candidates
- tables of precomputed hashs - drop this? 
19 
what can help with this is multi-factor authenication


- xxs / injection to take passwords
- dictionary attack to dehash it
- but then how to overcome the random key generator? 

20
sessions - period of time
session - tokens exchanged

token - an obj / string that maintains state between client / server
- it ties all requests to a single indivudal

two kinds of tokens - drop

return to this screen? 

24 
we get two tokens back
define each 

user validates
recieves two tokens
in this case 
rt - once
at - after 15


27
rt token stolen
it's used - either before

drop one of these timelines

jwt tokens vs opaque

hashing vs encryption


xxxxx

vpn - encrypts

Using a VPN (Virtual Private Network) to encrypt and tunnel the connection on your phone or mobile device is also advised. 

periodically clearing your browser and system caches will reduce the number of cookies you have available to steal.

- local solar - 

"server fell off the domain"

Because HTTP is stateless, in order to associate a request to any other request, you need a way to store user data between HTTP requests.

Cookies or URL parameters ( for ex. like http://example.com/myPage?asd=lol&boo=no ) are both suitable ways to transport data between 2 or more request. However they are not good in case you don't want that data to be readable/editable on client side.

The solution is to store that data server side, give it an "id", and let the client only know (and pass back at every http request) that id. There you go, sessions implemented. Or you can use the client as a convenient remote storage, but you would encrypt the data and keep the secret server-side.

Of course there are other aspects to consider, like you don't want people to hijack other's sessions, you want sessions to not last forever but to expire, and so on.

factors for canceling

session can expire or renew after 

- idle time - min without activity
sessin time - mins regardless of activity

Store poisoning
attacker can hack a CA (store) + insert bogus certificates
or change the keys on on a certificate


classess

javascript.info
mtutation-bserver
constructor-new
property-accessor
https://www.javascripttutorial.net/es6/javascript-class/

google tables

https://tables.area120.google.com/u/0/workspace/aepaKt9-wHE8gZQ7fk34PH/table/85H6gAvd8456V2qfppc_pH

terry gilliam

grohl foo fighters drummer girl

Broken authentication is an umbrella term for several vulnerabilities that attackers exploit to impersonate legitimate users online
 
Browsers
Firefox has a list of 147 trusted root certificates, representing 52 organizations, 
macOS has 168 root certificates, representing 60 organizations, 
Windows has 255 root certificates, representing 101 organizations.

 

 

opens it to an attack



html ewweb storage - stop

OWASP Mobile Top 10
 
 
  
  GEORGIA 17




6
stopped page 10 
 . 
 

9 - 
one article dsicussed an incident where 
a but was found in an extension to OpenSSL
open source cryo 
the extension was called heartbeat
it checked for 
so the bug was called heartbleed
move to end of chapter

10 

 
Any sharing Points

moving on to session - 

creatomg a sessopm defomtopm [age]

18

 
19
- number

after session fixation

session-based vs token-based auth

whereas session-based auth relies on session ids 

token-based auth relies on JTW-token (access token)

+ session-token (refresh token)

Used in responsive - 

21 change title : access + refresh

JWT tokens / session ids

