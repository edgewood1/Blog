security
- lock doors
- freedom from, resilience against harm
- don't limit thining to software: physical, financial, info
- patterns: 
  - authenticiation: are you who you say you are / showing yr id
  - authorization: what you're able to do... 

  technology: camera, 
  practices: screening, checking locks before crashing
  people (most important): design, maintain, operate

  custom agent catches potential terrorist becasue follows up on her intuition

  frank abagnale - con-man - 

  bruce schneider

  people building
  - training
  - develop a security mindset - awareness (email...)
  - 

  security theater
  - provides the feeling of improved security while doing little to achieve it (no fly list).
  
  owasp - 

  https://owasp.org/www-community/

  there's also crypto

  attacks 70
  - what someone might do
  vulnerabilities 60
  - weakness in yr app
  control
  - patching, automated security scanning, verifying vendors, training developers.

  code injection attack takes advantage of a buffer overflow vulnerability
  sql injection attacks takes advantage of improper data validation vulnerability
  not a 1-1 necesarily


  attacks
  
  lesson 1 - how to stand

all software component does I/O (socket, file, etc) possibel target - more IO , larger attack surface area

how ot minimize this surface

lots of I/O - 

2003 - easy out of box
2008 - nothing works, you configure everything / minimizes attack 

cs behind hospital's firewall, but can be hacked from inside
some servers not firewall

public cloudish - future

address bar

HL7 listener and router enabled by default - 
- this is a bad thing.
- why is it bad for it to be on by default.

forcing someone to turn on something means they're aware of it.
 
- no one's aware that something is tramitting, and so its not made secure

- deserializing - when u read data - like json, xml, a socket, anytime you do i/o you get data from one format to another - put strings around it? be careful regarding what's in that string and you read a file, and its corrupt or malformed, what should we do? wrong extenion - zip to json > 


- socket i/of

message based - message 


sockets - read streams of bytes

dicom bytes come through socket to form a pdu / 

first - handshaking section in payload

sanity check - restrict // 

- put limits on

type checks - 

check for sane pdu length values

beware
- just trying to get x done
- careful around lenght fields

deserialization of untrusted data 

- converting... 


engingeering > secure software

NEXT MEETUP

https://www.horangi.com/blog/real-life-examples-of-web-vulnerabilities

https://owasp.org/