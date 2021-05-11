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
`./` before the name of the file.

So we execute the file by typing `cat ./-` This gives us the password for the next level,which happens to be-`CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9`.

## level 2
using the method from previous levels you can login into this level.
Here we can see that we have a file called `spaces in this filename` so whenever we want to access the files with spaces in the name we should quote it then we can open the file. \
So to execute this file what we have to do is put quotes around the name of the file.
`cat 'spaces in this filename'` this gives us the password for next level which is
`UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK`

## level 3
again we login to this level as bandit3 and hit ls to see what it contains
we can use the cd function to navigate to the directory 'inhere' and see what it contains
we try the `ls` function but we see that there is nothing present. \
now try the `ls -a` function which also shows the hidden files or files whose names start with a `.`,  
thus we can see that a file called `.hidden` which gives us the password for next level.  
Password:`pIwrPrtPN36QITSp3EQaw936yaFoFgAB`.

## level 4
So we know that here we want to find the only human readable file is the one that we need to find. So lets login into the level and see what we see there. \
Ok so here we have 10 files here so lets see what option in the `file` command we can use to find this particular file. 

so to use this `file` function we need to check every file name. but we know that all the files have `./-file` common in there name so we can iterate over the files having this as a part of their names to see what kind of file they are if they are of the form ascii then that is the file we are looking for: \
So we type the command `file ./-file*` and we get the output : 

	./-file00: data
	./-file01: data
	./-file02: data
	./-file03: data
	./-file04: data
	./-file05: data
	./-file06: data
	./-file07: ASCII text
	./-file08: data
	./-file09: data

Thus we can see that `./-file07` is the one containg the password so we execute it to get the password: `koReBOKuIDDepwhWk7jZC0RTdopnAYKh`

## level 5
so now to find this file we need to understand what properties that the file needs to have.
it has to be of type ascii,not executable and of size 1033 bytes which is represented by `1033c`. 

so lets see the options that we need to add to the `find` function for this search to work, 
1. `-size 1033c` for the size constraint
2. `-type f` cause it is a human readable file.
3. `! -executable` so that it is not a executable file.
so together we would put the command together and it would look like:  

`find ./ -size 1033c -type f ! -executable`  

we get the output:`./maybehere07/.file2`

hence we execute this file to get the password for next level  \
`DXjZPULLxYr17uwoI01bNLQbtFemEgo7`

## level 6

so here again we are given some properties to take care of while finding the file that we are searching for based on that we should execute this particular command:  

`find / -group bandit6 -user bandit7 -size 33c -readable`  

based on this we get this particular output:  

	find: ‘/root’: Permission denied
	find: ‘/home/bandit28-git’: Permission denied
	find: ‘/home/bandit30-git’: Permission denied
	find: ‘/home/bandit5/inhere’: Permission denied
	find: ‘/home/bandit27-git’: Permission denied
	find: ‘/home/bandit29-git’: Permission denied
	find: ‘/home/bandit31-git’: Permission denied
	find: ‘/lost+found’: Permission denied
	find: ‘/etc/ssl/private’: Permission denied
	find: ‘/etc/polkit-1/localauthority’: Permission denied
	find: ‘/etc/lvm/archive’: Permission denied
	find: ‘/etc/lvm/backup’: Permission denied
	find: ‘/sys/fs/pstore’: Permission denied
	find: ‘/proc/tty/driver’: Permission denied
	find: ‘/proc/20792/task/20792/fd/6’: No such file or directory
	find: ‘/proc/20792/task/20792/fdinfo/6’: No such file or directory
	find: ‘/proc/20792/fd/5’: No such file or directory
	find: ‘/proc/20792/fdinfo/5’: No such file or directory
	find: ‘/cgroup2/csessions’: Permission denied
	find: ‘/boot/lost+found’: Permission denied
	find: ‘/tmp’: Permission denied
	find: ‘/run/lvm’: Permission denied
	find: ‘/run/screen/S-bandit27’: Permission denied
	find: ‘/run/screen/S-bandit2’: Permission denied
	find: ‘/run/screen/S-bandit14’: Permission denied
	find: ‘/run/screen/S-bandit16’: Permission denied
	find: ‘/run/screen/S-bandit22’: Permission denied
	find: ‘/run/screen/S-bandit4’: Permission denied
	find: ‘/run/screen/S-bandit31’: Permission denied
	find: ‘/run/screen/S-bandit24’: Permission denied
	find: ‘/run/screen/S-bandit21’: Permission denied
	find: ‘/run/screen/S-bandit0’: Permission denied
	find: ‘/run/screen/S-bandit25’: Permission denied
	find: ‘/run/screen/S-bandit23’: Permission denied
	find: ‘/run/screen/S-bandit20’: Permission denied
	find: ‘/run/shm’: Permission denied
	find: ‘/run/lock/lvm’: Permission denied
	find: ‘/var/spool/bandit24’: Permission denied
	find: ‘/var/spool/cron/crontabs’: Permission denied
	find: ‘/var/spool/rsyslog’: Permission denied
	find: ‘/var/tmp’: Permission denied
	find: ‘/var/lib/apt/lists/partial’: Permission denied
	find: ‘/var/lib/polkit-1’: Permission denied
	/var/lib/dpkg/info/bandit7.password
	find: ‘/var/log’: Permission denied
	find: ‘/var/cache/apt/archives/partial’: Permission denied
	find: ‘/var/cache/ldconfig’: Permission denied 

here i was able to identify this particular line which did not say permission denied.
`/var/lib/dpkg/info/bandit7.password`  

lets execute this file and hence we get the password: `HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs`.  

So what if we dont want to find this manually and just want to get the output that does not show permission denied then we use the command `2>file` this command redirects the files through `stderr` which checks the output if it is true then it returns the file which does not give any errors like permission denied.  

this function `>file` returns `stdout` if no other argument like `2` is passed to it, it also gives `stdout` if `1>file` is passed.  

`/dev/null` is the null device it takes any input you want and throws it away. It can be used to suppress any output.  

Basically it just takes an input and passes it out so when we use it with the `2>` we pass the input through the stderr to compare it.  

so when we pass this command:  
`find / -group bandit6 -user bandit7 -size 33c -readable 2>/dev/null`  
output :`/var/lib/dpkg/info/bandit7.password`

on executing again we get the password.

## level 7

Now we know that we need to search for the line containing the word `millionth` in the text document `data.txt` which is there on this server. 

So if we want to find a particular word in text document we use the `grep` function which we use to find that particular text which we want. 

This gives us the key or the password we are looking for: `cvX2JJa4CFALtqS87jk27qwqGhBM9plV`

Thus we have the password for the next level. 

## level 8

Here we have many text lines and we want to find the line which has not been repeated.
I have found two ways to solve this problem so let us use this partcular function `uniq` which we can use to find the text which is not repeated. 

First way of using this is using it with other functions.

`cat data.txt | sort | uniq -u`

here we use the sort function to put together the common keys together so we can find the unique key easily then we use the function `uniq -u` which gives us the text line which is not repeated at all.

This gives us the password `UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR`

Another way of solving this problem is by counting the no of times a particular line is repeated then searching for the line which has a frequency of only one which also gives the expected key or password.

For this we will use the command `cat data.txt | sort | uniq -c | grep '1 '` in this the 
`uniq -c` is used to count the frequency the lines then `grep '1 '` is used to find the line with frequency 1.

This gives the output : `1 UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR`

## level 9
Ok for this level we have been told that the password is preceeded by a number of `=` so one way to solve this problem would be by brute force basically executing this file and looking for it manually which does work after some effort.

So on using this method the password appears to be:`truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk`

Another way of solving this problem would be by using `grep` function along with the `strings` function: \
`strings data.txt | grep '='`

This gives us the output:

	========== the*2i"4
	=:G e
	========== password
	<I=zsGi
	Z)========== is
	A=|t&E
	Zdb=
	c^ LAh=3G
	*SF=s
	&========== truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk
	S=A.H&^

Here we can see that the password is `truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk`.

Hence the porblem is solved.

## level 10
The password for the next level is stored in the file data.txt, which contains base64 encoded data.

So this is the problem statement,So we can see that this is encoded text in the base 64 so to convert it into normal language we have to use the command `base64` which has a decoder which can be used to get access to the text that we desire to find.

`base64 data.txt -d`

This gives us the output:

`The password is IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR`

Thus we have the password for the next level.

## level 11

So for this problem we are going to use the transalte command which is `tr` so what this can be used for is to translate the given letters into the required text based on the substitution cypher which has been put into place.

So we will execute the `data.txt` and then pass it through our translator which is \
 `tr [A-Za-z] [N-ZA-Mn-za-m]`

 So the command will be:

 `cat data.txt | tr [A-Za-z] [N-ZA-Mn-za-m]`

 This gives us the output : `The password is 5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu`

 
