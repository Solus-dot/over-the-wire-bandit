# over-the-wire-bandit
```
Name: Sohom Chakraborty
Roll no: 231016
Department: BT BSBE (Y23)
```
<br/>

Level 0: (password: bandit0) <br/>
For this we just need the SSH command to long on to shells. They will ask for the password which is given in the site itself. 

```
ssh bandit0@bandit.labs.overthewire.org -p 2220
```
<br/>

Level 1: (password: NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL) <br/>
As we are in the bandit0 shell, we will see the files we have in the home directory with the `ls` command. we see there is a file called `readme`. We view it.
```
> cat readme
NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL
```
<br/>

Level 2: (password: rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi) <br/>
Here we are logged in as the user bandit1. This is same as level 1 but the file is now called `-` so to access is we simply write `./-`.
```
> cat ./-
rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi
```
<br/>

Level 3: (password: aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG) <br/>
This is the same as level 1 and 2 but now the filename is `spaces in this filename` so we can open it as `spaces\ in\ this\ filename`
```
> cat spaces\ in\ this\ filename
aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG
```
<br/>

Level 4: (password: 2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe) <br/>
Here we go to the `inhere` directory and find the password in the hidden file. to find the hidden file we use the `ls -a` command.
```
> cd inhere
~/inhere> cat .hidden
2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe
```
<br/>

Level 5: (password: lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR) <br/>
We only have one human-readable file in the inhere directory. So to find that, we use the `file` command to see the data type of all the files and to do it all together we use the wildcard character `./*` that scans every file.
```
~/inhere> file ./* 
``` 
We find the file that has the data type `ASCII text` written beside it.
```
~/inhere> cat ./-file07
lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR
```
<br/>

Level 6: (password: P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU) <br/>
The question says the file is human-readable, non executable and 1033 bytes in size, so we can just use the `find` command to search for it.
```
~/inhere> find . -type f -size 1033
./maybehere07/.file2
~/inhere> cat ./maybeher07/.file2
P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU
```
<br/>

Level 7: (password: z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S) <br/>
This is similar to Level 6, but it is owned by user bandit7 and owned by group bandit6. We can use the `find` command again from the root (`/`) directory and change the conditions, we can also redirect the stderr (2) stream to some file in the tmp folder (as we might get a lot of permission denied errors).
```
> find -type f -size 33c -user bandit7 -group bandit6 2>/tmp/foobar
/var/lib/dpkg/info/bandit7.password
> cat /var/lib/dpkg/info/bandit7.password
z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S
```
<br/>

Level 8: (password: TESKZC0XvTetK0S9xNwm25STk5iWrBvP) <br/>
Here, the password is in a very big file after the word `millionth`, so we can just pipe the output to grep to find the line containing the word.
```
> cat data.txt | grep millionth
TESKZC0XvTetK0S9xNwm25STk5iWrBvP
```
<br/>

Level 9: (password: EN632PlfYiZbn3PhVK3XOGSlNInNE00t) <br/>
For this level we sort the file and then use `uniq -u` to find the line that has only occured once.
```
> sort data.txt | uniq -u
UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR
```
<br/>

Level 10: (password: G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s) <br/>
We find the printable strings of the file using `strings` and then we pipe this output to grep to find the lines with a lot of `=` signs.
```
> strings data.txt | grep ====
x]T========== theG)"
========== passwordk^
========== is
========== G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s
```
<br/>

Level 11: (password: 6zPeziLdR2RKNdNYFNb6nVCKzphlXHBM) <br/>
We get the string `VGhlIHBhc3N3b3JkIGlzIDZ6UGV6aUxkUjJSS05kTllGTmI2blZDS3pwaGxYSEJNCg==` when reading the data.txt file and know that it is base64 encoding, so we just decode it to get the password.
<br/>

Level 12: (password: JVNBBFSmZwKKOP0XbFXOoW8chDz5yVRv) <br/>
This is a simple ROT13 substitution in the file with the string 
`Gur cnffjbeq vf WIAOOSFzMjXXBC0KoSKBbJ8puQm5lIEi` translating this gives us 
`The password is JVNBBFSmZwKKOP0XbFXOoW8chDz5yVRv`
<br/>

Level 13: (password: wbWdlBxEir4CaE8LaPhauuOo6pwRmrDw) <br/>
This is a tricky one and I needed help with this. Here we get a hexdump file we need to check with the `xxd` command. First we make a temporary folder and move the hexdump there
```
> mkdir /tmp/foobar
> cd /tmp/foobar
/tmp/foobar> cp ~/data.txt dump.txt
```
Looking at the hexdump files, we see that the compressions are in the order of gzip, bzip2, gzip, tar, bzip2, tar, gzip. After decompressing we finally get the final data file:
```
/tmp/foobar> cat data8
The password is wbWdlBxEir4CaE8LaPhauuOo6pwRmrDw
```
<br/>

Level 14: (password: We need a private SSH Key) <br/>
In this level we are provided a file call `sshkey.private` which we have to use instead of the password to log in to the next level. We copy the file from the shell to our local machine using `scp`, we change the permissions of the file using `chmod 700` to make it less open and then we enter the next leveling using the following command:
```
ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220
```
<br/>

Level 15: (password: jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt) <br/>
We are supposed to send the password to the port 30000 of the host we do that using netcat. previous level told that the password must be in the `/etc/bandit_pass/bandit14` file.
```
> cat /etc/bandit_pass/bandit14
fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq
```
Now we just input this password on port 30000 of the localhost.
```
> nc localhost 30000
fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq
Correct!
jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt
```

