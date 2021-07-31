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

 ## level 12

So here what we do is check what file contains so here it basically contains a hexdump which is hexadeciamal representation of the binary file.So when we execute this file we get:

	00000020: 2653 598e 4f1c c800 001e 7fff fbf9 7fda  &SY.O...........
	00000030: 9e7f 4f76 9fcf fe7d 3fff f67d abde 5e9f  ..Ov...}?..}..^.
	00000040: f3fe 9fbf f6f1 feee bfdf a3ff b001 3b1b  ..............;.
	00000050: 5481 a1a0 1ea0 1a34 d0d0 001a 68d3 4683  T......4....h.F.
	00000060: 4680 0680 0034 1918 4c4d 190c 4000 0001  F....4..LM..@...
	00000070: a000 c87a 81a3 464d a8d3 43c5 1068 0346  ...z..FM..C..h.F
	00000080: 8343 40d0 3400 0340 66a6 8068 0cd4 f500  .C@.4..@f..h....
	00000090: 69ea 6800 0f50 68f2 4d00 680d 06ca 0190  i.h..Ph.M.h.....
	000000a0: 0000 69a1 a1a0 1ea0 194d 340d 1ea1 b280  ..i......M4.....
	000000b0: f500 3406 2340 034d 3400 0000 3403 d400  ..4.#@.M4...4...
	000000c0: 1a07 a832 3400 f51a 0003 43d4 0068 0d34  ...24.....C..h.4
	000000d0: 6868 f51a 3d43 2580 3e58 061a 2c89 6bf3  hh..=C%.>X..,.k.
	000000e0: 0163 08ab dc31 91cd 1747 599b e401 0b06  .c...1...GY.....
	000000f0: a8b1 7255 a3b2 9cf9 75cc f106 941b 347a  ..rU....u.....4z
	00000100: d616 55cc 2ef2 9d46 e7d1 3050 b5fb 76eb  ..U....F..0P..v.
	00000110: 01f8 60c1 2201 33f0 0de0 4aa6 ec8c 914f  ..`.".3...J....O
	00000120: cf8a aed5 7b52 4270 8d51 6978 c159 8b5a  ....{RBp.Qix.Y.Z
	00000130: 2164 fb1f c26a 8d28 b414 e690 bfdd b3e1  !d...j.(........
	00000140: f414 2f9e d041 c523 b641 ac08 0c0b 06f5  ../..A.#.A......
	00000150: dd64 b862 1158 3f9e 897a 8cae 32b0 1fb7  .d.b.X?..z..2...
	00000160: 3c82 af41 20fd 6e7d 0a35 2833 41bd de0c  <..A .n}.5(3A...
	00000170: 774f ae52 a1ac 0fb2 8c36 ef58 537b f30a  wO.R.....6.XS{..
	00000180: 1510 cab5 cb51 4231 95a4 d045 b95c ea09  .....QB1...E.\..
	00000190: 9fa0 4d33 ba43 22c9 b5be d0ea eeb7 ec85  ..M3.C".........
	000001a0: 59fc 8bf1 97a0 87a5 0df0 7acd d555 fc11  Y.........z..U..
	000001b0: 223f fdc6 2be3 e809 c974 271a 920e acbc  "?..+....t'.....
	000001c0: 0de1 f1a6 393f 4cf5 50eb 7942 86c3 3d7a  ....9?L.P.yB..=z
	000001d0: fe6d 173f a84c bb4e 742a fc37 7b71 508a  .m.?.L.Nt*.7{qP.
	000001e0: a2cc 9cf1 2522 8a77 39f2 716d 34f9 8620  ....%".w9.qm4.. 
	000001f0: 4e33 ca36 eec0 cd4b b3e8 48e4 8b91 5bea  N3.6...K..H...[.
	00000200: 01bf 7d21 0b64 82c0 3341 3424 e98b 4d7e  ..}!.d..3A4$..M~
	00000210: c95c 1b1f cac9 a04a 1988 43b2 6b55 c6a6  .\.....J..C.kU..
	00000220: 075c 1eb4 8ecf 5cdf 4653 064e 84da 263d  .\....\.FS.N..&=
	00000230: b15b bcea 7109 5c29 c524 3afc d715 4894  .[..q.\).$:...H.
	00000240: 7426 072f fc28 ab05 9603 b3fc 5dc9 14e1  t&./.(......]...
	00000250: 4242 393c 7320 98f7 681d 3d02 0000       BB9<s ..h.=...

First of all we make a directory as told in the question as we will be decompressing a bunch of times.

So we start by converting the hexadecimal file into a binary file so to do this we use the function `xxd`.

`cat data.txt | xxd -r >data` This stores the binary form of the file into file called data.

So now we want to check what type of file is this data so we type `file data` which gives us the output: `data: gzip compressed data, was "data2.bin", last modified: Thu May  7 18:14:30 2020, max compression, from Unix`

Thus we change the name of the file to `data.gz` using the function `mv` then decompress the file using  `gzip -d data.gz` command.
This again gives us a file called data now when we see what type of a file it is,It says: \
`data: bzip2 compressed data, block size = 900k`

Thus we cange the name of the file to `data.bz2` and then decompress it again using the command:
`bzip2 -d data.bz2` This again gives a file data.\

Now we check the type of file and it returns: \
`data: gzip compressed data, was "data4.bin", last modified: Thu May  7 18:14:30 2020, max compression, from Unix`

So we change the name to data.gz and then decompress it again using the command: \
`gzip -d data.gz` Which again gives us the data when we check the type of file:
`data: POSIX tar archive (GNU)`

We change the name to `data.tar` and then decompress the file using the command \
`tar -xf data.tar` Which gives us a file called `data5.bin`.
This again is of the same type as before so we repeat the process and get `data6.bin` 
Which is of the type bzip2 so we use the command to decompress it.

These kind of decompressions are performed a few more times and then finally a file called 
`data8` is obtained which is of the type ASCII, thus we execute this file and we get the text displaying the password as `The password is 8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL`.

## level 13

So first we login into the server as bandit 13 and we check what and all files are there here:

here we see that there is a file called `sshkey.private` and we get to know that this is the rsa key that we can use to login into the next level.
So we type the command \
`ssh bandit14@localhost -i sshkey.private`

This will login us into the system as bandit14 now we need to execute the file which contains the key to this level.

Thus the key will be obtained using the command : `cat /etc/bandit_pass/bandit14` \

We obtain the password `4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e`

## level 14

So in this level we have to connect to the localhost at port no 30000 so to do this we have to use nc that is netcats in order to get the password. \

So we type the command `echo "4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e" | nc localhost 30000`

Thus we get the password for the next level that is : \
`BfMYroe26WYalil77FoDi9qh59eK5xNr` 

