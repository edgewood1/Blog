
__git permissions__

ssh-add ~/.ssh/elsevier
Enter passphrase for /Users/dejesusm1/.ssh/elsevier:
Identity added: /Users/dejesusm1/.ssh/elsevier (dejesusm1@ELSPHIM-219409)
dejesusm1@ELSPHIM-219409 monorepo %

pw: github11


vim filename



Cool git functionality

LIST YOUR LAST FIVE OPENED BRANCHES
git branch --sort=-committerdate | head -5

CLEAN ALL BRANCHES
git remote update --prune && git branch -vv | awk '/: gone]/{print $1}' | xargs git branch -D

prune dangling objects

How to solve the "too many dangling objects" problem?
1. git fsck
This will verify the connectivity, validity of the object and list those dangling objects if they exist.

1. git gc --prune=now

git prune
This will remove dangling objects.

git gc

-prune=<date> Prune loose objects older than date (default is 2 weeks ago, overridable by the config variable gc.pruneExpire). — prune=now prunes loose objects regardless of their age and increases the risk of corruption if another process is writing to the repository concurrently; see “NOTES” below. — prune is on by default.

submit_buy //product-code is md, but undefined for puchase

for second purchase, bought with same account and breakpoint didn't hit, but and product code was different.
new user:
product_code: md_mdcliscib2c for a submit_buy event
'mdcliscib2c'



product_code:
'MDCliSciB2C'