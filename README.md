# over-the-wire-bandit

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

