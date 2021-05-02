# BANDIT WRITEUP 

This is basically a wargame which we can use to learn the working of the terminal by exploring the commands.This writeup that i have written is from the perspective of a newbie as even i have recently started to explore the world of ctfs and cybersecurity.
I am maintaining this blog so as to get a better understanding of the concepts and so that it can be a help to others as well.
Enjoy the read :)

## level 0
Here we have to use the secure shell i.e ssh to login to the server i.e given to be
`bandit.labs.overthewire.org` we aere asked to join this at the port number `2220` using username `bandit0` and password `bandit0` so we just login using the ssh command after reading about the command ssh in the man pages.\
So we use the command:`ssh bandit0@bandit.labs.overthewire.org -p 2220` to join the server as bandit0 at port 2220 -p is the option used to port.

we can see a readme file in this folder so lets execute it to see what it says.\

`cat readme`

this gives the output i.e is the password for next level.
`boJ9jbbUNNfktd78OOpsqOltutMc3MY1`

## level 1
ok so for this level again we have to login into the server but this time with the username bandit1 and password we found in the last level 
`ssh bandit1@bandit.labs.overthewire.org -p 2220`
so enter the password that we found in th last level to login and you will be in.
the file that is present is a dashed file so files starting with - can be opened only by using 
`./` before the name of the file.\

So we execute the file by typing `cat ./-` This gives us the password for the next level,which happens to be-`CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9`.

## level 2
using the method from previous levels you can login into this level.
Here we can see that we have a file called `spaces in this filename` so whenever we want to access the files with spaces in the name we should quote it then we can open the file.
So to execute this file what we have to do is put quotes around the name of the file.
`cat 'spaces in this filename'` this gives us the password for next level which is
`UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK`

## level 3
again we login to this level as bandit3 and hit ls to see what it contains
we can use the cd function to navigate to the directory 'inhere' and see what it contains
we try the `ls` function but we see that there is nothing present.now try the `ls -a` function which also shows the hidden files or files whose names start with a `.` thus we can see that a file called `.hidden` which gives us the password for next level. 
Password:`pIwrPrtPN36QITSp3EQaw936yaFoFgAB`.

