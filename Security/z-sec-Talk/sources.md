
https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview

stopped at basic asptects of http

https://developer.mozilla.org/en-US/docs/Web/API/Web_Authentication_API

sessions http

https://en.wikipedia.org/wiki/Session_(computer_science)

misc

https://developer.mozilla.org/en-US/search?q=broken+authentication

videos 

https://www.youtube.com/watch?v=O3YktuvsYDk

https://www.youtube.com/watch?v=l0_LtN_g6vg

https://owasp.org/www-project-top-ten/

tokens vs sessions/cookies

https://www.youtube.com/watch?v=o9hT7v0OLJc



man in teh middle attack - your requests are channeled elsewhere 

https://www.youtube.com/watch?v=qXLD2UHq2vk

watch next: 

https://www.youtube.com/watch?v=q9vu6_2r0o4

good - general broken auth

https://www.youtube.com/watch?v=mruO75ONWy8

very good - 

https://www.youtube.com/watch?v=R1iGRBG3PJ8

https://www.youtube.com/watch?v=RASD0amPAXQ


a jwt looks like a series of digists
run it through an algorhthm

https://www.youtube.com/watch?v=_XbXkVdoG_0
videos

cookes vs tokens

https://stackoverflow.com/questions/17000835/token-authentication-vs-cookies

https://wp-rocket.me/blog/difference-json-web-tokens-vs-session-cookies/

process - https://www.youtube.com/watch?v=T4Df5_cojAs

broken auth

ovrview - https://www.youtube.com/watch?v=j8Yxff6L_po


certifcate

https://support.google.com/chrome/answer/95617?visit_id=637386666393537905-936061342&p=ui_security_indicator&rd=1

david crabbe

https://www.youtube.com/channel/UCvbcflqUK7Jwuv7EWPsfLtw/videos

http

https://developer.mozilla.org/en-US/docs/Web/HTTP

https://developer.mozilla.org/en-US/docs/Web/HTTP/Authentication

https://stackoverflow.com/questions/3487991/why-does-oauth-v2-have-both-access-and-refresh-tokens

best refer3ence

https://pragmaticwebsecurity.com/articles/oauthoidc/refresh-token-protection-implications.html

lyaters

https://www.altexsoft.com/blog/engineering/web-application-architecture-how-the-web-works/

tls - diagrams

https://www.google.com/search?q=tls&rlz=1C5CHFA_enUS863US864&sxsrf=ALeKk02u7Bk-wK7OBn_MEmadEjUHtB2AVA:1603380812022&source=lnms&tbm=isch&sa=X&ved=2ahUKEwi6xfX9wsjsAhXGY98KHbvtCAYQ_AUoA3oECE4QBQ&biw=1920&bih=912#imgrc=HRTlhAblWkylOM

one site can't access local storage for another site you visited
if malware on cpu? can jump into local storage.. 

third party auth

recaptcha prevetns bombard attacks

sources
https://stackoverflow.com/questions/17000835/token-authentication-vs-cookies


csrf token - https://stackoverflow.com/questions/5207160/what-is-a-csrf-token-what-is-its-importance-and-how-does-it-work

That’s why it’s also really important not to store JWT on the client, say via cookies or localstorage. Doing so you make your app vulnerable to CSRF & XSS attacks, by malicious forms or scripts to use or steal your token lying around in cookies or localstorage.

https://hasura.io/blog/best-practices-of-using-jwt-with-graphql/





OAUTH - spec for securing access to api servers.  specifices how tokens are transfered: https://aaronparecki.com/oauth-2-simplified/
oauth about authorization ... between services.. 

https://www.oauth.com/oauth2-servers/background/

===================

https://stackoverflow.com/questions/3487991/why-does-oauth-v2-have-both-access-and-refresh-tokens

