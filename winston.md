WINSTON


cable.logError(err) in loggError


winstonLogError(
 

console.trace(‘check’, info)


fs.post(‘v8/user’)  in log

Cable.logError

Redact // looks for values in object - 

request.index 

Where does msg become object

Windsotn.logError, passes in whole object as message

When logger.error(e) is called - the e is an object

Cable winston log updated to allow other parameters.. 

Elk formatting

Typeof info.message not a string
console.trace… 

Routes/www/post/logError 
- generates error message via 3 parameters
- string: js
- $P object
- $P.args object (this contains the error message


If local/osmosis/app/errorReport.js:29  has a msg error of the string: Uncaught SyntaxError: Invalid or unexpected token
- Transforms the combines the arguments into a single object
- Passed into Winston.logError()

Config/winston/logError

Logger.error(arg, arg2) will create an object that looks like : 
{message: arg, level: ‘error’, ….stuff from format.combine(), … arg2}

This creates the following: 

This is wrapped ina.  Message object and it shouldn’t be. 
{
  message: 'Uncaught SyntaxError: Invalid or unexpected token',
  level: 'error',
  service: 'osmosis-service',
  timestamp: '2022-11-21T20:55:41.883Z',
  [Symbol(level)]: 'error',
  [Symbol(message)]: '{"level":"error","message":"Uncaught SyntaxError: Invalid or unexpected token","service":"osmosis-service","timestamp":"2022-11-21T20:55:41.883Z"}'
}

fs.post request — where is the error object being generated.  

Go up a level - go up a structure of ‘e’ // 

logger.log({ level, message });logger.log({ level, message });
 

When the object gets to logError, it looks ok - msg: “” is at root, but lacks level

If goal is to have message + level at root.  

  userID: 1,
  session: 'rsOn4d7GaI0Z+07YqdfXZrw5',
  timestamp: 2022-11-22T20:51:41.844Z,
  level: 'error',
  message: 'Uncaught SyntaxError: Invalid or unexpected token',

≠

Winston p2

 getWinstonBase exported as winston
Calling it returns a local logger
Logger created by calling winston.createLogger(filter())
We call logger.error to log
We mock the logger

logger = winston.createLogger(etc);




logError is what outsiders call to log
It creates a logger via getWinstonBase
And calls logger.error

If we mock getWinstonBase to return an error function

We came across that back in June, but left the test alone bc of the idea that it was better to check if it had to do with a missing test env variable related to timezone preference. 

Che questions

- Way to clear all branches
- Mocking the db 
- Issue
- jest.mock before / after the import

Import db

Var db = require(‘osmosis/db’) — implies osmosis/db/index.js

Index uses directory mapper 
When app loads it’s going to look in the directory, __dirname

Const blog - require(‘./blog);
module.exports = {
Blog

Referencing each file as a property on this object.  

Jest.mock(‘osmosis/db’, () => jest.createMockFromModule(’osmosis/mockdb’);

Mine was a manual mock

Still define the mock

db_user_profiles.get.mockReturnValue({type.etc})

Mocked?db file


getlallwatchedbyuser: jest.fn()

… later

Const db= requier(‘osmosis/db’);

Db.elearn_watdhed.mockReturnValue({]

Mocks get refreshed with each test… 

Check what’s being returned 

Auto-mock > does every item in a file, or every file in a directory 

Manual mock - define what to mock yourself.  

Automock

jest.mock(osmosis/db) - goes through and checks methods returned and auto setup mock function.. 

Db is a special case - jest.mock won’t work because of index file… 

logError function
If / else … instead  add a return statement

Fi () {…. Return;}. God function- lots of if satatements
GOT closure
Guard clauses… 

DevIQ - design patterns… 

Log support — same

If () {
Do this
Return [message, meta]

If () {
}

Remove let statement… 


Message, mettle >> return an object
An array - order matters
An object - order doesn’t matter…. 

Get message only returns the message

Getmetadata only returns meta data -  only about deleting meta message… 


Be careful about deleting stuff - 
- Instead return an object of copy
Return { …msg, e: […msg.e, message: undefined]


But generally don’t need 

Logsupport

Want message = msg.emessage, not what I have.

Instead use optional chaining

Return msg?msg || msg?.e?.message | msg?.err.message || msg (in case 
Double vertical lines 

If first one exists return, else move on 

This can just be put in logError… 

Does logError

winston.logError(e) move msg back into redact… 

Then copy redact

&& msg.msg … get rid of msg.msg —— 


For error instance
logger.error(msg.message, { stack: msg.stack })

Run testError.file — resurrected that.. 

Get rid of string return since exception 

logger.error(msg) at the end


For two if
Return logger.error(message, msg)

Object will have the optional chaining… 

If you’re returning different 

Test 

Import log error from the file

Remove winston from winston.logError

jest.mock winston library

Winston and logError from ./winston
Don’t have to delete winston library itself… 

====