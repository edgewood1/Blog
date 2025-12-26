security talk - marcus

1. opening screen 1101
2. web 101  1103

db --- server --- browser
          ^
          static files: html js css images

browser > http > server

http - request resopnse protocol
it involves a request message
- request line, header fields, an optional body
- http verbs: put get update
- safe methods > 
- browser uil bar performs a get request
- forms perform post request

response message: 
- status code, headers, optional

example request
GET / HTTP/2
Host: cs-feature-stable
"host" is a headeruser-agent > 
accept:  - what responses are accepted: text/htmlcookie - add all cookies 

3. client side tech - 4 terms > 1114
- html
- js
-css
- dom

4. visual of dom 1115 (demo)1117

5. web app types 1122

traditional - 
hybrid
spa - 

6. xxs - what is it 1127
- attack / on what version of owasp
7. why dangerious? 1129
- js can access all objects on page, modifying, accessing apis like microphone, and files
- without right protection on cookie, then it can be taken
- set up a server and have site data sent to a server.
- redicrects to malicious website
- 

types of xxs 1132

reflected - unvalidated and unescaped user input

url 
? - doesn't define a location but a means of passing extra info to a server

example: https://www.ex.com/search?text=<script>alert(1)</script>

POST data > type in password click submit and data goes to another server

instead of alert they insert script that will post data elsewhere


stored xxs - stores unsantizied user input that is viewed at a later time by another user > comment section of blog, type in script tag and javascript - if not sanitized, the js will run when viewed - it renders script tag as real html. profile data.  


dom xxs - 1146 - 
sink functions accept unparsed strings and parses it into a script or dom to be evaluated immdiatedly
- inneerHTML, plugins, setTimeout or new Function() - 

runtime js code  copilation - settimout, new functions, eval
generating html - innerhtml, iframe??? 

prevention 1151
- litelement auto sanitizes

1156 - how should we change how we think - 
- know limitations of yr framework
- react overrides sanitization > 

csrf notes
- tricks victim into submitting a malicious request
- caues state change on server

cookies - data stored on user's cpu by browser from visiting website
- used for auth / tracking
- set cookie on client with session immdiatedly
- now client requests include session immdiatedly
- server figures out what state associated with htmlcookie

- different from a token

user
same origin concept 
if user setups up custom page on their forms
submit to webpage. 

csrf token - onetime