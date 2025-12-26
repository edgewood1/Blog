

access control system - a mechanism that regulates access to data or functionality by dtermining wehther a subject is permitted to perform an operation on a target.  can I view my ballance in my bank account? 

acm relies on two processes
- authenticatio - proving that you are who you claim to ballance
- auhorization - figuring if you have the rights to do what you want to do
- protected data - what i'm after
- sensitive functionality - what i want to do

3 ways of authneicating - we can use: 
- something you know: password
- something you are: fingerprint, retinal pattern, hand geometry, face topography (biometrics)
  - not easily re-issued or reclaimed.
- something you have: digital certifcate, smart card, google authenticator

2 factor authnication - using two of the above methods. 

password authenticatio
- http spec provides two built-in mechanism: Basic and Digest access authenticatio
- sign-on solutions: windows live id and facebook connect. 
- custom auth systems

Basic
- type username / password
- concatted with a colon
- base64-encoded and submitted via GET under the Authorization header
- Auhorization: Basic 34j2oi4u23o04u23

* user can intercept values an decode because it is not encrypted.  instead better to submit over an ssl connection or othe rencyrpted medium
* creds must be submitted wiht every request for protected resources.  creds are cached and resubmitted.  thsu creds exposed repeatedly with each request
* the browser caches the auth creds.  insecure storage.  no session is created so no way to invalidate a session.  thus, no way to log out.  to clear sotred creds, is to close tab / clear history.  (cache-control headers can prevent a client browser from cacheing admin pages locally on client's cpu.  )

response.setHeader("Cache-Control","no-store"); - there's also private or no-cache
response.setHeader("Pragma","no-cache");

cache - a means of temp storing frequently accessed static content, like teh same web content.  web cache can serve content rather than the origin server.  this improves repsonve time. whenever content is downloaded its stored in teh web cache for a set period of time determined by caching rules you set.  

1. a suer calls site, browser sends http request to web cache, if not there, it requests it from the origin server.  if present, info can be used without a network connection. 

how do web sites store data on users' computer? client-side storage
dynamic sites store data on server via db (server-side storage), and retrieve via server-seide code. , insert into stage page templates, and serve the resulting html to client.  
client-side stoage - JS api's that allow you to store data on client (user's machine).  - allows personalizing site preferences (color scheme, font size), persisting previous site activity, saving assets and docs. download music. 
old school: cookies.  used for session ids and access tokens
new school: 
web storage  - user's name, time logged in, color of screen - these are objects.
indexedDB api - a complete db system for storing complex data like sets of records, autio/video files
new new: 
cache api - http responses to specfic requests - stores website assets offline so the site can used them without a network connection.  used with the server worker api.  

https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Client-side_web_APIs/Client-side_storage

__DIGEST__

same as basic but it uses the MD5 hashing algorithin to transform teh password before its sent.  
problems - man-in the middle attack: the client can be tricked to downgrade the security back to basic auth .  

single sign-on auth (SSO) > lastpass

- user logs in to a single interface and gains access to many independent securid systems.  
- last password
- corporate intranets
- google acciounts - log into google mail > youtub, etc. already done for you.  

custom auth systems- ev dcodes own app logic to process creds. most populaar
process1. request login page
- web app returns it
- user enters creds into form, browser includes form fields as part of http post request
- upon receipt, web app parses / extracts us password
- app queries back-end data store to check password and returns wrong or...
- a session started with user via creating a session id value and returning it to user via a cookie in http response: 
- set-cookie: jsessionid == asld;kfj209js
- when browser gets this, it observes set-cookie directiveand stores the value of the session id, submitting it alongside all requesets. 
thus we have persistent auth

how to validate creds? 

consider location of comparison logic
- within the app? > app sends sql query to backend db, gets record, comparies record to the plaintext pw successfully, then valid
within the database? 
- the db will compare pw if record found.

in the app with hashed pw - req made to back, get record for username, user paword is hashed using the ame algorithm that was used to hash the stored password - thus they are compared.  if two hashes are equal then. 

in db - has sent pw on arrival and send it to db, whcih does the coparison.  
google: is lastpass secure
https://www.lastpass.com/security/what-if-lastpass-gets-hacked

securing password  based auth
attacks against password

offline attacks - script that hashes variou swords until it matches the hashed pasword value.  - this requires you have the has password value.  

dictionary attack - a long list of password candidates.  this list and permutations will be used in a an offline attack.  

brute force attack - an exhaustive key search - used in offline attacks against hashed password values

the longer and more complex the password the longer to crack
a good one coule take 60 days, but if you changed your password monthly... 

min length
min complexity
pw uniqueness
avoid stored password, but if you must, use strong hashing with salt and roundes

- don't store plaintext
- don't encrypt, cause then you must store the key
- hash via a one way transform., stored in database.
- we use an algorithm, not a key, to hash.  
- salt - a random value that's tossed into the algorithm - thus two identical passwords would result in different hashes. 
- put a password through multiple roundsof hashing (standard is 10K times) p80


- 
- 