# Consolidated OS Docs

## OS/os/1.os-shell.md

kinds of hardware? 
- physical (computer)
- virtual (virtual computer) - server space + basic functionality to accept an OSs


computer
- hardware
- os - hardware/app interface
- apps - MS office 

os (parts)
- kernel - loader pogram, drivers, task-manager, access, memory handler, system calls, security
- utilities - Utility software is system software designed to help analyze, configure, optimize or maintain a computer. It is used to support the computer infrastructure in contrast to application software, which is aimed at directly performing tasks that benefit ordinary users: Disk Cleanup, defragmenter, system restore, disk compression, registry cleaners, file splitters,  A device driver is a program that controls a particular type of device that is attached to your computer. There are device drivers for printers, displays, CD-ROM readers, diskette drives, and so on.
- shell / terminal - terminal is an i/o device + shell is the interpretation program.  shells run on terminals

shell (kinds)
- bash, zsh, fish
- powershell, cmd

os (kinds)
- windows (evolved from DOS kernel... Xbox uses this too)
- unix
  - linux (ubuntu, )
  - macos
 
 
GUI - a software package that provides a desktop, shortcuts to applications, a web browser and a media player

  This shell accepts commands, so we can learn bash commands that interact with the linux-unix OS.  They translate the commands into commands that the UNIX core will understand. 

Shell scripting is simply taking all the commands you would type in to do something and putting them in a text file so you don't have to type them in every time. 

A lot of "bash scripting" is really knowing how to compose and use the standard Unix utilities (find,ls,sort,grep,etc..). 


shell 
- a comand-line interpreer provides a command line UI
- a language
- provide piping, variables, conditions, iteration. 
- used by os to exectute system elements via scripts
- interact with the shell using a terminal emulator

ways to access shell

- terminal emulato
- connect via SSH what is a SSH client (in terminal?)

2 sets of shell script syntax

1. Bourne - more flexible / popular.
- bash, sh, zsh, ksh
2. C shell syntax 

Apple replaced bash with zsh as defaul shell in macOS ~

--- 

## OS/os/env-var.md

https://medium.com/chingu/an-introduction-to-environment-variables-and-how-to-use-them-f602f66d15fa

--- 

## OS/os/macos_files.md


Three levels

1.	Root (MacHD)
a.	Applications
b.	Developer
c.	System
d.	Library
e.	Users > goes to HOME*
f.	Volumes > external drives
g.	Data > db > mongo collections
h.	Etc
i.	Usr > *
j.	Var
k.	Bin – this has bash commands
Second - Tier
2.	Home (your name)
a.	Deskop
b.	Bash files
c.	pgadmin
3.	Usr
a.	Local  *
b.	Share *
c.	Bin
d.	Sbin
e.	Include
f.	Lib
Third-tier
1.	Local 
a.	Bin
b.	Cellar
c.	Etc
d.	Frameworks
e.	Git
f.	Homebrew, 
g.
Mysql
h.	Share 
i.	Var > mongodb, mysql keys, postgresql, pg_etc
j.	Lib > nodemon, postgresql, pthon 3.6/2.7, ruby, heroku
2.	Share – 
3.	Lib
a.	Cron
b.	Php
c.	Python2.7, ruby, sqlite3, shortcuts
d.	zsh

--- 

## OS/os/process-thread.md

Terms
A function in itself might be a small set of instructions, but it might not be a thread. 
A thread requires that a user interact with the program in order to do something – puruse a new course of action.  So the program being open and my typing into it represents one thread of control.  

Threads share the same address space
Each thread has own instruction sets, specfiic tasks, own stack memory, instruction pointer, only share address space, sharing global variables and memory space. 

Multithread – accomplishes many things almost at the same time.  But two set s of execution with own register and stack.  So independent.  

Multiprocesses / cpu cores (processors).  

 the CPU is shared among running processes or threads using a process scheduling algorithm that divides the CPU’s time and yields the illusion of parallel execution. The time given to each task is called a “time slice.” The switching back and forth between tasks happens so fast it is usually not perceptible. The terms parallelism (genuine simultaneous execution) and concurrency (interleaving of processes in time to give the appearance of simultaneous execution), distinguish between the two types of real or approximate simultaneous operation.


Concurrency – many lines on one task, many tasks
Paralelism – one line on one task, many tasks.

Register – a storage site / location - holds an instruction, storage process, or a piece of data
Counter / instruction pointer  – tells where it is in process.  A stack pointer. 
Stack – data type – stores info about the active subroutines of a computer program - a collection of elements, usually held in a register? 

Processes have their own addresses spaces. 

Unless they use a share interprocess communcation technique. 
1.	Thread –  a small set of instructions that can be executed.  A line of control coursing through the program.  A thread of control moving through.   A thread of execution.
a.	Single – only having one long chain of instructions
b.	Multi – having many chains of instructions processed at once
i.	These might conflict if two wants to read / write same data. 
2.	Process – an instance of an app and state fo all threads executing in the program.
3.	Concurrency – having multiple “workers” (threads?) processing a single chain.
a.	The last part might finish first, or last, and the result should be the same? 
4.	Parallelism – having multiple chains being processed by multiple “workers”
5.	Synchronous – one step ONLY after the next.
6.	Asynchronous – can skip steps and come back to those later
a.	Step 1 - get records
b.	Step 2 – do some math
c.	Step 3 – say goodbye
d.	Step 4 – when records appear give finish the math and send.  

What is a single-threaded application? 

A program (like Notepad.exe) is a passive collection os instructions stored on secondary memory or a disk.  When executed, the kernel reads it into primary memory and executed.  

A process is the actual execution of these instructions.  It is an instance of a computer program that is being executed.  

**When you double click on a notepad icon (execute it), a process is started that will run the notepad program.  This is an active entity, residing in primary memory.

A process could refer to: 
1.	Each instance of notepad running on cpu.  You could have 5 docs open. 
2.	A different application – you could have 1 instance of notepad and one of windows running.  

windows Task Manager shows a list of the various processes currently running on your computer. 

A thread is a chain of commands being processed.  

A single-thread implies one command must wait for the previous to finish.

Concurrent – running at same time / parallel
Concurrency – You have a single chain of commands.  thread1 runs through steps 1-3, thread 2 runs through steps 4-6, thread 1 finishes the steps. 
Parallel – You have two chains.  one thread runs through one chain while another runs through a second chain – advance is simultanesous

At the high level Node.js falls into the category of concurrent computation. This is a direct result of the single-threaded event loop being the backbone of a Node.js application. 

A thread is a component / part of a process.  A process is made up of many threads. 

Single-thread – processing of one command at a time.
Multi-threading - 

Several processes can execute concurrently, sharing resources like memory. 

 A process can be made up of mulitple threads executing instructions concurrently

It’s the ability to process only one command ata time.  It is the oppoite of multi-threading, which is the ability to execute many threads within the context of a single process. 

A thread is a “mini-process” – a “sequence stream” within a process

Threads shares the same address space, yet have own instruction set, own instruction pointer, own stack memory, own global memories. 

Word doc process:
Thread 1 – the OS takes user inputs
Thread 2 – the OS prints  a document
Both share memory of the process. 

 
JAVASCRIPT IS SINGLE THREADED, however, theres ASYNCH, which allows parallelism > 

 Synchronous – porcess runs only asa result of some other process being completed or handing off operatios.  A file is sent, a response is sent with success or resend.  8**  it blocks a process til the operation completes.  In send/receive context, aoperation is completewhen messages delivered to reciever.  Or when prcoss finsihes executuion.  

Not every blocking operation is synchronous, and vv – I may send while people wait for other to receive, but if other has not received it, it is not synchronous.  

Asynchronous – two events that occur at different times – having to wait until the other is finished – so Consecutive, which is the opposite of concurrency.  They are not coordinated in time.  ** a process operates independnt of other processes. --- this is a non-blocking and only initaties the operation – the caller can discover completion by some othe rmechanism.  

Asyncrnous allows more parallellelism – it can do computation while messaage is in transite.  

Async – process can receive messages on many ports simultanesouly
Synch – fork different processes for each concurrent operation – yet costs extra process management. 

Asynch proclems – what if a message can’t be deliverred? Send may not wait for delivery of message and so not hear the error.  So we need a way to notify an asynch reciever that a message has arriveed.  

Node.js is a single-threaded application BUT it can support concurrency via EVENTS and CALLBACKS

Each API is ASYNCHRONOUS – that means they are non-blocking – 3 threads may be occuring at once – 

Because it is SINGLE-THREADED, it uses asynch function calls to maintain concurrency.  

Node thread keeps an event loop and when a task gets completed, it fires the corresponding event w hich signals the eventlistener function to execute. 

When node begins, it initiates variables and functions, then waits for events to occur. 

There is a main loop that listens for evetns, and then triggers a callback function when one of those events are detected.  

1.	Event


An event – things like moving the mouse, clicking, etc. 
An event handler – this is a detecting process.   – it listens for an event to happen, when it does, it directs the flow to the call back.  So, event handlers control callbacks. 

The event manager is told: push button, fire callback

Callback – a function passed to a procedure, to be “called” or “used” (like, shared) at some point in that procedure. 

An event handler is a procedure called when an event happens. ... An event handler is a type of callback. It's called whenever an event occurs. The term is usually used in terms of user interfaces where events are things like moving the mouse, clicking something and so on.

1.	Callbacks are called when an asynch function returns its result
2.	Event handling works on the observer / listener pattern.  When an event gets fired, its listener function starts executing.

--- 

## OS/os/threads.md

https://www.google.com/search?q=thread+os&rlz=1C5CHFA_enUS743US743&oq=thread+os&aqs=chrome..69i57j0i512l4j69i60l3.3221j0j7&sourceid=chrome&ie=UTF-8

--- 

## OS/shells/bash/bash-basics.md


filepermissions

owner-group-others

digiit adds: 
4 - read / 2- write / 1 - execute

755 means rwx for owner, rx for both others.

combine commands 

same line comamands - use semicolons between

&& - code placed after this will only run if previous command completes successfully

|| - continues if previous commands fail

create video folder only if cd command s fails

cd~/videos || mkdir ~/videos

navigation

cntrl-
a - move caret to start
e- to end
k - deletes all characters after
u - all characters in front of the caret
L - clears screen 
c - cancel

less - pagination

directing output

instead of printing to conosle
output of command could go into a file

x > y

pipe

pass output to another command

x | y

grep 
- searches


example - find all pdfs and output them using less

ls | grep ".pdf" | less

--- 

## OS/shells/bash/bash-config.md

**bash_profile / bashrc  / bash history**

`.bash_profile` is executed for login shells

When you login (type username and password) via console, either sitting at the machine, or remotely via ssh: `.bash_profile` is executed to configure your shell before the initial command prompt.

`.bashrc` is executed for interactive non-login shells.

But, if you’ve already logged into your machine and open a new terminal window (xterm) then `.bashrc` is executed before the window command prompt. `.bashrc` is also run when you start a new bash instance by typing `/bin/bash` in a terminal.

On OS X, Terminal by default runs a login shell every time, so this is a little different to most other systems, but you can configure that in the preferences.

- create custom commands in bash_profile (or both?)

**gitconfig, gitflow_export, gitignore_global**

zshrc / zsh_history

vscode

ssh

**Where are these found?**

1. Root - system, users, bin, home, usr
   1. users
      1. meldejesus
         1. .bashrc
         2. .bash_profile
         3. .bash_history
         4. .gitconfig
         5. .gitignore_globoal
         6. .gitflow_export
         7. .zsh_history
         8. .zshrc
         9. .vscode
         10. .ssh



--- 

## OS/shells/bash/bash-links.md


sleep 3
printf '[OK]\n'

grep -i '31 passing' test-suite-log2.txt > new.txt
echo '31 passing'; grep '31 passing' test-suite-log2.txt  | wc -l

 bash

 https://tldp.org/HOWTO/Bash-Prog-Intro-HOWTO-4.html

 gnu

 https://ftp.gnu.org/old-gnu/Manuals/grep-2.4/html_node/grep_7.html

 count

 https://stackoverflow.com/questions/2908757/count-number-of-occurrences-of-a-pattern-in-a-file-even-on-same-line

 stdout

 https://www.computerhope.com/jargon/s/stderr.htm#:~:text=Stderr%2C%20also%20known%20as%20standard,defaults%20to%20the%20user's%20screen.

 loop 

 https://www.tecmint.com/run-repeat-linux-command-every-x-seconds/

 output

 https://askubuntu.com/questions/420981/how-do-i-save-terminal-output-to-a-file

 npm node_modules
 https://stackoverflow.com/questions/25045946/where-should-my-npm-modules-be-installed-on-mac-os-x

Creat an alias function

https://stackoverflow.com/questions/7131670/make-a-bash-alias-that-takes-a-parameter

https://medium.com/devnetwork/how-to-create-your-own-custom-terminal-commands-c5008782a78e

--- 

## OS/shells/bash/crud-files.md

bash

**CREATE**

touch file
mkdir folder

**READ**

cat file

**DELETE**

remove all contents of a folder

rm /path/to/directory

**recursive remove**

the '-r' flag also removes sub directories/files and prompt you for each

**force remove**

add '-rf' flag to skip prompts

add an _ to the end if you want to keep the folder but just remove contents
above, but also preserve interior folders: rm -f /path/to/{_,."}
 
 **UPDATE**

copy a file / make a backup

cp /source /destination

rename a file

mv /original /newName

--- 

## OS/shells/bash/variables.md

bash 

How do I test if a variable is a number in Bash?

What you've written actually almost works (it would work if all the variables were numbers), but it's not an idiomatic way at all.

(…) parentheses indicate a subshell. What's inside them isn't an expression like in many other languages. It's a list of commands (just like outside parentheses). These commands are executed in a separate subprocess, so any redirection, assignment, etc. performed inside the parentheses has no effect outside the parentheses.
With a leading dollar sign, $(…) is a command substitution: there is a command inside the parentheses, and the output from the command is used as part of the command line (after extra expansions unless the substitution is between double quotes, but that's another story).
{ … } braces are like parentheses in that they group commands, but they only influence parsing, not grouping. The program x=2; { x=4; }; echo $x prints 4, whereas x=2; (x=4); echo $x prints 2. (Also braces require spaces around them and a semicolon before closing, whereas parentheses don't. That's just a syntax quirk.)
With a leading dollar sign, ${VAR} is a parameter expansion, expanding to the value of a variable, with possible extra transformations.
((…)) double parentheses surround an arithmetic instruction, that is, a computation on integers, with a syntax resembling other programming languages. This syntax is mostly used for assignments and in conditionals.
The same syntax is used in arithmetic expressions $((…)), which expand to the integer value of the expression.
[[ … ]] double brackets surround conditional expressions. Conditional expressions are mostly built on operators such as -n $variable to test if a variable is empty and -e $file to test if a file exists. There are also string equality operators: "$string1" == "$string2" (beware that the right-hand side is a pattern, e.g. [[ $foo == a* ]] tests if $foo starts with a while [[ $foo == "a*" ]] tests if $foo is exactly a*), and the familiar !, && and || operators for negation, conjunction and disjunction as well as parentheses for grouping. Note that you need a space around each operator (e.g. [[ "$x" == "$y" ]], not [[ "$x"=="$y" ]]), and a space or a character like ; both inside and outside the brackets (e.g. [[ -n $foo ]], not [[-n $foo]]). 
[ … ] single brackets are an alternate form of conditional expressions with more quirks (but older and more portable). Don't write any for now; start worrying about them when you find scripts that contain them.
This is the idiomatic way to write your test in bash:

if [[ $varA == 1 && ($varB == "t1" || $varC == "t2") ]]; then
If you need portability to other shells, this would be the way (note the additional quoting and the separate sets of brackets around each individual test, and the use of the traditional = operator rather than the ksh/bash/zsh == variant):

if [ "$varA" = 1 ] && { [ "$varB" = "t1" ] || [ "$varC" = "t2" ]; }; then

--- 

## OS/shells/unix/study_unix.txt

study unix book

Environment variables hold values related to the current environment, like the Operating System or user sessions.

what are other env variables? 

PATH is an environment variable specifying a set of directories where executable programs are located.

holds all bin and sbin

----------------------------

33

absolute pathname begins with the root directory and follows the tree to the desired file.  

the root directory: /usr/bin

relative pathname begins with working directory. uses special notation
. (dot) - working directory
.. dotdot - working directory's parent directory. 

usr/bin
cd .. - goes back to usr (cd /usr)
cd ./bin - goes back to usr/bin (cd usr/bin)
 -- above ./ is implied so can be omitted.

ls -a - shows hidden files too? 

? ls  List directory contents
? file  Determine file type
? less  View file contents

ls -l : reveals format of directory (permisions, etc - long format)

ls -t: sort the result by the file's modification time.

ls -lt - two options. 

commands: 

commmand -options arguments


long listing fields
-rw-r--r-- > access rights to file. 

--- 

## OS/shells/linux.md


Linux

Shell – program that takes commands to perform on OS. 

First steps
1.	Directories
2.	Files
3.	File contents
Shell examsion
1.	Commands and arguments
2.	Shell variables
3.	Shell history
4.	File globbing
Pipes and commands
1.	i/o redirctions
2.	filters 
3.	basic unix tools
4.	regex
vim
1.	–
Scripting
1.	Variables
2.	Loops
3.	Parameters
User management
1.	Basics
2.	Passwords
3.	Profiles
4.	Groups
File security
1.	Standard file permissions
2.	Access control lists
3.	File links

http://linux-training.be/linuxfun.pdf

https://www.howtogeek.com/412055/37-important-linux-commands-you-should-know/

http://linuxcommand.org/lc3_lts0010.php


classes / objects



 http://linuxcommand.org/lc3_lts0010.php

--- 

## OS/shells/unix.pdf

<Content from PDF file OS/shells/unix.pdf>

--- 

## OS/virtual/2.virtual.md

A droplet is a virtual server and a VM

A virtual server is an off-site server with shared resources

A vs operates in a multi-tenant environment - so many VMs run on the same physical hardware. 

Vs is a way of server hosting using VM. 


Can containers and VM work together?

- docker can run on a VM too 
- if networked right, docker can interact with a VM 
- Kubernetes orchestrates containers.  Docker uses this.  

VM uses a hypervisor - software running the OS
Docker uses a docker daemon instead, running its images... 
 
https://www.youtube.com/watch?v=pGYAg7TMmp0


Docker has two parts
1.	Client
2.	Server, which runs a virtual machine

image - a file with paired down OS + 

Commands

Exit - leave a container
Docker images - see all images

What is shown on 'docker image': 
- Repo - where it comes from
- Tag - version
- Image id - a reference

* Refer to its by repo-tag or imageId

Lessons

don't let your containers fetch dependencies when they start
instead make containers contain dependencies themselves

don't leave important things in unnamed stopped containers - because you'll delete a seemingly unimportant containers.. 


- hyperV is a kind of VM 
- networking for developers on youtube
- cloud basics
- 

virtualization
- os only runs on specific kind of hardware - it seeks it out as an input
- you can run software that mocks the hardware, so that the os runs on it. 
- virtualization layer talks to hardware to get what's needed for the OS

What makes things different from VM

- On a VM, I can add files, and when I reboot, they are still there.
- An image is fixed. Like a snapshot. I can add files to a container, but if i create a second container from original image, the file won't be in it.  

--- 

## OS/virtual/docker/0_background.md

# Steps

1. write Dockerfile
2. Build Image from this file
3. make sure it exists
4. Run Image



cardio server

npm install node-sass
npm run styles




--- 

## OS/virtual/docker/1.intro.md

image - a file with all  deps / configs needed to run a program

container - image instance / program

docker for mac
1. docker client (CLI) - we will enter commands into terminal and this will manage them.  doesnt do anything with images, etc.  just a means of interacting

2. docker server (daemon) - creates images, etc.  it recieves commands from the client.  

install docker for mac

docker version

using docker client

=======


run commands on docker client
processes them and sends to docker server

`docker run hello-world`

start a new container using image of 'hellow-world'
this image has a program inside to print otu xyz

run command.
docker server sees we're startign to start a container
check if there's a local copy in the image cache.  no?
so go to docker hub repo (free images for doownload).
does this image live there? yes!~
download hellow-world file
stores it in image cache
container is image instance whose purpose is to run 1 program
docker creates a container and runs single program inside of it

what is a container? 

__how does os run?__

chrome, terminals, spotify, node
make system calls to kernel
kernel makes calls to cpu, memory, hard disk

nodejs > kernel > hard disk

kernel intermediary between software / hardware
system calls are like function calls
kernel exposes endpoints that can be called


what if 
chrome requires python v2
nodejs requires python v3
yet hard disk only has v3
and we can't have both at same time. 
thus only nodejs would work.

namespacing 
- segmenting the hard drive
- assigning oen segment to house one app (python v2 vs v3)
- make sure one app is assigned to one segment
- kernel makes this decision: if app1 calls harddrive, call directed to segment 
- thus node / chrome can work on same machine. 
- isolate resources per process


control group 
- limit amount of resources used per proces
- resources: memory, cpu usage, hd i/o, network bandwidth

container
- an isolated app, the kernel, segment of [HD, network, RAM, CPU]

What is image vs container? 

image
- single file w/ list of deps and config required to run program
- consists of FS snapshot (chrome/python)
- + startu command
- fs snapshot placed into a segment of HD
- start up command, invokes file in HD, which runs a process

namespacing / controlgroups is a LINUX thing
yet running on macos / windows. 

When we install docker for mac, we installed a linux VM
inside VM all containers created
VM has a linux kernel that hosts containers 
each container is runnign a process

==== 
section 2 - 15

we use an image to create a container

docker - reference to docker client
run - create run container

docker run <image-name>

- creates container
- adds image to HD
- runs image as an instance-process


--- 

## OS/virtual/docker/1_steps.md

# Example

...
ADD ./test2.js /client/mobile1/
dockerfile
client1

- mobile1
  -test.js
- mobile2
  -test.js
  mobile1

  - test2.js
    test2.js

- if you do the current layout,
- it creates a client1, mobile1, and mobile2 root folder

RUN node client1/mobile1/test

RUN node client1/mobile2/test

WORKDIR /client/mobile1/

RUN node test.js

docker run - used to manipulate an images in local host


RUN cd mobile/ && npm run serve -- --target https://cs-next-deploy-12

CMD ["npm" "run" "serve" "--" "--target https://cs-next-deploy-12"]


CARDIO SERVER
- run container
- enter using exec
- npm install on both levels
- mobile: 
  - npm uninstall node-sass && npm install node-sass
    - run styles


--- 

## OS/virtual/docker/2.commands.md

```
 docker start [OPTIONS] CONTAINER [CONTAINER...]
```

```
docker compose COMMAND
```

```
docker compose start [SERVICE...]
```

- starts existing containers for a servcie
- starts / restarts all servies defined in docker-compose.yaml
- "attached mode - see logs from all containers"
- "detached" -d starts, exists, and containers run in background
- this never creates new containers, it only restarts ones that were stopped

```
docker compose up [SERVICE...]
```

- Build, recreates, starts, and attaches to containers for a service

```
docker compose run [options] [-v VOLUME...] [-p PORT...] [-e KEY=VAL...] [-l KEY=VALUE...] SERVICE [COMMAND] [ARGS...]
```

- running one-off tasks
- requires teh service name you want to run 
- used for tests, performing admin tasks
- 


```
 docker build [OPTIONS] PATH | URL | -
```

- reads dockerfile + a context to create a docker image. 
- context - files located in specified path / url



```
docker stop [OPTIONS] CONTAINER [CONTAINER...]
```

- docker stop my_container
- stops all services 
- does NOT remove any containers

docker-compose down

- stops all services
- Also removes any containers / internal networks
- NOT internally specified volumes - to do this, specify the -v flag after the down command


docker networking

lsof -i:8182

COMMAND  PID    USER  FD  TYPE       DEVICE SIZE/OFF NODE NAME

com.docke 1513 meldejesus 111u IPv6 0x12fe2d6492f58d8b   0t0 TCP *:8182 (LISTEN) 

```
kill -9 PID
```

--- 

## OS/virtual/docker/2.images.md

# build an image so that you can run it

docker build -t <name> .

# confirm the image's existence

docker images

# destroy an image

delete one image

docker rmi id (or name)

To delete all containers including its volumes use,

docker rm -vf $(docker ps -a -q)

To delete all the images,

docker rmi -f $(docker images -a -q)

or? 

docker image prune

------------other commands

#Format output

docker ps -l --format=$FORMAT // shows

## Saving Images 

run an ubuntu image, add a file, exit, then commit

docker commit id  name // will create another image named name

docker commit id name:v4 // v4 is the tag\ 

## Add a name to the image

docker tag <ID> my-image   // this will give the image a name 'my-image'  
 
docker commit my_file My_image2  // changes the name

--- 

## OS/virtual/docker/containers.md

# run the image; that is, create a "running" container
turns an image into a running container. 

docker run [flags] <name> [command]

[flags]

-ti / terminal interactive (a flag causes it to have a full terminal in the image so you can get formatting towers 
-t
-it > 
-d / detached mode / desgned to shut down right after entrypoint command 
--name [pickAname]
-p 8000:8000

[commands]

bash 

[examples] 

docker run -it newtest bash // run a non-running container bash to explore

docker run -d --name myapp4 -p 8000:8000 test

docker run -t -d centos

docker run -ti ubuntu:latest bash / this will run ubuntu:latest env and run the bash shell

__Docker ps__ shows all the running images

You can format vertical print using this flag: 

--format=$FORMAT (will show the ID) 

  - what it shows? 
      ID - container id
      Image: that made it
      Commond: that’s running in it. 
      PORTS - 
      NAMES - a reference name


# run a command in a running container? 

docker exec -it CONTAINER bash

$ docker exec -d ubuntu_bash touch /tmp/execWorks

docker exec d3067 ls

docker exec d3067 sh -c "cd mobile && ls"

# list your containers

docker ps // lists all running containers
docker ps -a // lists all containers

docker run -it newtest bash

docker run -t -d --net=host cardio 

# start / stop a container

docker container stop <name>

docker container start <name>

# destroy all unused containers 

docker container prune

**running things in docker**

docker run --rm (runs, then deletes contain after)

-ti ubuntus sleep 5 // starts container, sleeps for 5 sec, stops

docker run -ti buntu bash -c "sleep 3; echo all done"

-c // run various things

**how to leave something runnning in a container?**

docker run -d (detach - leave it running in background) -ti ubuntu bash  // this drops an id

new terminal: 

docker attach <names>  // this jumps into the container that's running

ctrl - p / contrl - q // detaches

**add a process to another container**

docker exec -ti <names> bash // this addds a new bash process (image) inside the other. 

**how to manage a container?**

docker logs <names> // see errors

docker kill <names> // container goes to the stop state

docker rm <names> // remove old / stopped container >> this keeps things from getting bogged down.

docker ps -l --format=$FORMAT // what is teh last to exit? 

-- stop containers still exist until you explicitly remove them

**resource constraints**

- ability to enforce limits to how many resources a continer will use

- memory limits
    docker run --memory maximum-allowed-memory image-name command
- cpu limits
    docker run --cpu-shares (10 % of use -relative to other containers / cpu time limit so others can share rest)
- hardlimits
    docker run --cpu-quota  (hard limits - to limit it in general)

--- 

## OS/virtual/docker/demo.md

A droplet is a virtual server – a production machine that spins up quickley.  It is a Linux-based virtual machine that runs on top of virtualized hardware.  A programming environment. 

Digital ocean, like AWS, is a “cloud-server”, or ‘cloud service platform’ that offers database storage, computer power, etc.  .  Others include google cloud, azure.  

The ‘cloud’ refer to a group of servers that can be used for hosting, data sharing, and softward use

Dgital ocean allows use to set up affordable linux instances called droplet.  

You can have many virtual machines running DO.  
Can you have many apps being served on each? 
A VM image is a blueprint / recipe of a particular VM environment
A VM instance is a running blueprint. 

Docker allows you to manage application processes in containers, which are processes that isolate resources.  

Containers and VMs are two ways to deploy multiple isolated services ona single platform.  Each VM will have its own OS, runtimesystem (node), and app.
A container manager will merely host varous runtimesystems (node) (java?) each withtheir app.
A runtime system is an engine that translates a given programming language or languages into machine code. 
My OS has a system of shared files, etc.  so I can run a 1 then another runtimesystem, and both are sharing all the same files systems, like local/bin, etc… 
A VM will create an OS-runtime that’s isolated from my physical system, on which I can build and run my app
A container will host a runtime system that’s also isolated, but which shares resources with the physcial OS. 
https://www.electronicdesign.com/dev-tools/what-s-difference-between-containers-and-virtual-machines

So why would I use docker containers on my VM that’s running a particular OS and runtime? 

Maybe I want to create a container in this VM in order to run Python backened? 

Essentially, docker is a containerization tool that provies software apps with a filesystem that container all that app needs to run.  If in a container, a piece of software will always behave the same way, regardless of where it is deployed, becaues its runtime environment is consistent.  

https://www.digitalocean.com/community/tutorials/working-with-docker-containers

https://www.vermasachin.com/posts/8-running-docker-containers-digitalocean/



DNS – go t godaddy DNS seetings and screae an entry to point back to digital ocean.  

remote dekstop also an option

--- 

## OS/virtual/docker/docker_installation.md

# Docker Installation

These instructions are presented as an alternative to installing MySQL directly onto your students' computers: it is included here because several students were unable to get MySQL installed on their local computers.  There is the added benefit that installing Docker opens up all kinds of possibilities with other databases, languages, and operating systems.

This is a more advanced option because it requires the use of a container technology [Docker](https://www.docker.com/).  Yes, introducing an additional layer of technology may mean that we are opening Pandora's box and letting out all sorts of new errors and obstacles.  However, the purpose of Docker is to _normalize the environment_.  Instead of trying to install MySQL on all variations of host machines (including Windows, Mac, and every possible variation of those operating systems that you will find in a classroom), we install the Docker virtual machine, and then we load up the _exact same_ MySQL image into it.  If your computer represents an angry ocean of unpredictable processes and permissions, Docker floats on top of it like a sturdy ship.  Instead of trying to install MySQL into the stormy waves of your desktop, we install it onto the deck of the ship.  You can think of the process something like putting a video game cartridge into a machine.  

> *CAREFUL:* It is not recommended to install both a native version and a Dockerized version of MySQL onto the same machine.  Doing so may result in port conflicts or other glitches that can be hard to troubleshoot.


## Install Docker

The specific product we are interested in is called "Docker Community Edition" (or "Docker CE" for short).  You may download it from the [Docker Store](https://store.docker.com/search?type=edition&offering=community).  Choose the installer for your computer's operating system (Mac or Windows).

You must create an account on the Docker Store before you can download Docker.  Choose a username and a password that you will remember (and store your password securely in a password management program). 

For more information about installing onto your particular operating system, you can review the specific instructions: 

- https://docs.docker.com/docker-for-windows/install/
- https://docs.docker.com/docker-for-mac/


## Starting Docker

Once you have successfully installed Docker, it may take a few minutes to start up.  There is a menu icon (a picture of a whale with shipping containers on its back) -- you will need to ensure that the Docker app is running every time you want to use an image that runs inside of Docker (think: you have to power on your Nintendo if you want to play Super Mario Brothers).  You can set system preferences to ensure that it starts on startup.

## Installing 

You can browse the [Docker Hub](https://hub.docker.com/) to find images to install into your Docker VM.  This is a lot like an app store: people and organizations submit images for all kinds of applications and technologies that you can download and run.  We are going to download the officially sanctioned Dockerfile for MySQL: [https://hub.docker.com/_/mysql/](https://hub.docker.com/_/mysql/)

> Docker is a command-line tool -- although the GUI tools for it are getting better and better, you should prepare yourself for running these commands from the command-line.

Run the following command in your terminal:

```
docker pull mysql:5.7.22
```

This specifies that we want the `mysql` image, and specifically the one tagged as version `5.7.22`.  You can omit the colon and the tag, and the latest version of the image will be assumed.

> Note the "pull" command... it looks and acts a lot like Git!  We are pulling down a Docker image in the same way we pull down a repo.

Keep an eye on the terminal to watch the progress update.  If you are somewhere with a slow internet connection this may take a while.


## Running MySQL

When we run MySQL for the first time, we need to give our instance a name.  For simplicity, the name `virtual-mysql` is used in these examples and we will continue to reference version 5.7.22 of the `mysql` image.

The following command sets the password of the root user to `root`:

```
docker run --name virtual-mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root -d mysql:5.7.22
```

This is a long command!  You should save it!  Bookmark it!  Make an alias for it!  This is what you will need to run each time you need to start your virtual MySQL container instance.

### Errors

If you get an error like 

```
docker: Error response from daemon: Conflict. The container name "/virtual-mysql" is already in use by container "89f1f7d82a5aefc00a5a6522f5d01df3059e5b09975d75bde197a69c8471e5e3". You have to remove (or rename) that container to be able to reuse that name. 
```

That means that your MySQL Docker container is already running!  No need to start it again!  


## Connecting to MySQL using a Client

Once your MySQL instance is running inside of its Docker container, you should be able to connect to it using a MySQL client.  

- *host*: 127.0.0.1
- *user:* root
- *password:* root
- *port:* 3306



### Host File

This shouldn't be required, but just in case you want to refer to your dockerized container by its hostname ("virtual-mysql"), you may wish to add an entry to your host file to explicitly declare the mapping.  Map your hosname of "virtual-mysql" to your localhost IP address of `127.0.0.1`.  Add an entry to your hosts file like the following:

```
127.0.0.1 virtual-mysql
```

On a Mac, the hosts file is located at `/etc/hosts` and you will require admin privileges to edit it.
On Windows, the hosts file is located at `C:\Windows\System32\drivers\etc`



## Shutting Down MySQL

At the end of the day, you may wish to shut down your instance of MySQL.  You do this using the `docker stop` command and supplying the name of your container:

```
docker stop virtual-mysql
```

--- 

## OS/virtual/docker/docker_mysql.md

create 

1. mysql image

docker run --name=test-mysql mysql

remove same one if needed to

docker rm test-mysql

initialize db and specify pw option


attached mode, which means you can't do anything else: 
docker run --name=test-mysql --env="MYSQL_ROOT_PASSWORD=mypassword" mysql

docker run --name=test-mysql --env="MYSQL_ROOT_PASSWORD=mypassword" mysql

detached mode: 

docker run --detach --name=test-mysql --env="MYSQL_ROOT_PASSWORD=mypassword" mysql

get teh IP address of the container so we can access it: 

$ docker inspect test-mysql

    "IPAddress": "172.17.0.4",

add volumes and connect the docker port to the host port


$ docker run \
--detach \
--name=test-mysql \
--env="MYSQL_ROOT_PASSWORD=mypassword" \
--publish 6603:3306 \
--volume=/root/docker/test-mysql/conf.d:/etc/mysql/conf.d \
mysql

--- 

## OS/virtual/docker/dockerFile.md

docker

https://blogs.umass.edu/Techbytes/2018/10/09/what-is-docker-and-how-does-it-work/

https://vsupalov.com/database-in-docker/

google:

problems with docker

can docker and vm work together

tutorial

https://diveintodocker.com/?utm_source=nj&utm_medium=youtube&utm_campaign=virtual-machines-vs-docker-containers

You can run a script, or a more complex parameter to the RUN. Here is an example from a Dockerfile I've downloaded to look at previously:

RUN cd /opt && unzip treeio.zip && mv treeio-master treeio && \
 rm -f treeio.zip && cd treeio && pip install -r requirements.pip

Because of the use of '&&', it will only get to the final 'pip install' command if all the previous commands have succeeded. 

google

docker exec multiple commands

docker localhost didn’t send any data. ERR_EMPTY_RESPONSE

pm WARN saveError ENOENT: no such file or directory, open '/client/mobile2/package.json'

mulitple package.json files in one container

https://stackoverflow.com/questions/56244081/how-to-change-file-path-for-package-json-in-docker

https://stackoverflow.com/questions/37415134/error-node-sass-does-not-yet-support-your-current-environment-windows-64-bit-w

sends info to VM
but has no way to handle?

what i did

create a container that opens to bash

navigate to mobile and run npm start

OR

we can just run

cheat sheet

https://github.com/wsargent/docker-cheat-sheet

--- 

## OS/virtual/docker/dockerLinks.md

container must link to host's  "network interface" 

vm exposes to the host machine , whcih can be accessed by teh container. 

https://docs.docker.com/network/

network modes
- bridge - a container started by default is created inside this network (docker0)
- host
- null

through bridge, we can connect to container's exposed port 

containers have internal and external ports

these are mapped to each other

-p 808:8080

** use the --network_host flag in the build: 

docker build --network=host

1. kill docker container / image
2. create new image with above flag
3. add npm styles, etc... 
4. run container... 

---quotes

For a quick work around you can run all the containers with flag --net=host which means the docker containers will use the host network interface. more info on docker networking can be found here. 

**Container network**

- programs in containers are isolated from the internet by default
- it offers private network so you can group containers together in a network yet isolated from rest of containers on computer
- you choosen who can connect to whom
- you can expose or publish a port to let connects in
- private networks to connect between containers

expose a port


internal port that the program is listening on
port listening on the outside. 

terminal 1 - create a server

- start server that accepts data from one client and passes it to another
(inner:outerport)
docker run -p (port#:connectedtoport#) -p (port1:port1) --name echo-server ubuntu:latest bash

once your in the bash terminal of an ubuntu os, run: 

net-cat utitilty a network debugging portramm for moving bits from one place to the next
nc -lp 45678 | nc -lp 45679
data passed in on one port and spit out on another port

terminal 2 - first client

nc localhost 45678

terminal three

nc localhost 45679

terminal 2, type "let's go"

this will go from  2 -1-3

how to get an image that runs netcap if don't have it locally

just run an ubuntu image, that has it. 

host.docker.internal >> this refers to the machine hosting everyone

nc host.docker.internal 45678

in terminal 3 / run same container and run corresponding nc host... commmand

above we implicitly exposed port

if you want to run many ports, expose dymanically

leave off the host side of port definition, and docker will fill it in from one of the available ports

the port inside the container is fixed, the port on the host is chosen from the unusded ports,  this allows many containers running program with fixed ports


same as aobve but only one port per -p

nc -lp 45678 | nc -lp 45679

on other termianl: 

docker port echo-server // 3277

this tells you the assigned outer ports
hook up to these with other terminals using netcap

nc localhost 3277, etc... 

abov e is tcp, but you can use udp... 

____

docker bridge

1. ethernet port
2. IP Tables / NAT - Network address translation is a method of remapping one IP address space into another by modifying network address information in the IP header of packets while they are in transit across a traffic routing device.  Map a port on the host side to a port on the container side.  
3. Docker Bridge - handles communication between containers to host or between containers.
   1. containers... 

User defined bridges - prevents containers from talking to eachother unless they go through host

overlay networking - no NAT.  


docker network ls 

shows all networks

all containers are connected to work

the bridge is the means by which the container can talk to the external world.  
the bridge can be configured via the --net flag
there are four modes: 
The --net default mode
In this mode, the default bridge is used as the bridge for containers to connect to each other.

The --net=none mode
With this mode, the container created is truly isolated and cannot connect to the network.

The --net=container:$container2 mode
With this flag, the container created shares its network namespace with the container called $container2.

The --net=host mode
With this mode, the container created shares its network namespace with the host.

--- 

## OS/virtual/docker/networking.md

Load an image on a virtual box

Both provide isolated environments.  

Docker – a container is an isolated set of processes running from an image that provides it with files.  The containers share the host OS kernel.  Used to isolate individual applications.  Smaller and faster. – better for dev cycles and microservices.  Yet they don’t do true vitualization – you can’t run a windows container on a linux host? Easy to change. Share the same kernel with the host os but comes with a larger surface for possible attackers… to hack.  

Apartment that has shared plumbing and faciliteis with its surrounding apartments

VM – consists of user space + kernel space of an OS.  – used to isolate entire systems.  Uses hypervisors.  A full system.  A VM doesn’t interact with the HOST OS – there is a “hypervisor” layer between them.  The machine is running its own guestOS and several applications within it. 

Houses that has its own plumbing

OR 

Implement Dcker using a virtualmachine.  

https://www.freecodecamp.org/news/comprehensive-introductory-guide-to-docker-vms-and-containers-4e42a13ee103/
nested containers

https://medium.com/@peorth/using-docker-with-virtualbox-and-windows-10-b351e7a34adc

--- 

## OS/virtual/docker/vm_docker.md

Volumes -- virtual discs to store and share data

sharing data between container
w kinds: 
persistent - data there after container gone
ephemeral - data exists as long as being used by container

- not part of an image / used for local data only

shared folders with the host
sharing a single file into a container 
both similar

mkdir example
docker run -ti -v /path/to/example/folder:/path/withincontainerwhere folder can be found (/shared-folder/) ubuntu bash

inside contain ls /shared-folder/
touch shared-folder/my-data
exit 
ls example/ --> data will still be there

shared data between containers (epheremeral)

create a volumen not shared with host
docker run -ti -v /shared-data ubuntu bahs
echo hello > /shared-data/data-file
docker ps to get name
docker run -ti --volumes-from sick_hopper ubuntu bash

sick_hopper is the name of the machine that has the volumes I want to use. 

ls /shared-data

you'll see the data-file.  

opwn  2ES XONRinwe -- 

docker registries

pieces of software that manage and distribute images
upload and download and search images here. 
docker search ubuntu // this will show a lot
hub.docker.com // do a search here... 

docker pull debian:sid // pulls debian image

docker tag debian:side mel/test-image  // changes the name

docker push mel/test-image /// pushes file to docker 

--- 

## OS/virtual/docker/volumes.md

# Define your image directory

WORKDIR /a - begins with a slash, so it is the absolute path
WORKDIR b - lacks a slash, so it is a relative path. This is the same as /a/begins

# copy your files to the image

COPY . /a/ -- absolute path to a
COPY . b/ -- relative path to b
COPY . /a/b/ -- absolute path to b

If i have
/client/mobile1
/client/mobile2

WORKDIR /client/mobile

COPY . /client/

WORKDIR /client

COPY . /client
COPY . /client/mobile

will that create a client/mobile directory just like the original?

# what's teh difference between copy and add?



###

-------

build images with code 

dockerFile - small programs to create an image
run program

docker build -t name .

t means tag 
. > in current directory (place to find docker file)
else show path

when it finishes the result will be your local docker registry

each line takes the image from previous line and makes another image
the previous image is unchanged
it does not edit the state from prev line

see dockerfile reference

caching with each step

process you start on one line with not be running on the next line

ENV command  will be set on the next line

FROM busybox (name of image) // create image
RUN echo 'building simple docker image'// 
CMD  echo 'hello container'

docker build -t build .

each line above creates a container
which results in a final container
and the image for this is committed

syntax
from - starting point
maintaner - name and email 
run - run a command in this shell
add - add files or contents of tar archives and urls (things you download from a url)
env - set env var for duration of docker file and when running the result 
entrypoint - specifies the start of teh command to run / lets u tack more later.. 
cmd - specifies whole command to run 

```