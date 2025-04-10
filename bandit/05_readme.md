# [Bandit Level 4 → Level 5](https://overthewire.org/wargames/bandit/bandit5.html)

## Goal
The password for the next level is stored in the only human-readable file in the inhere directory. Tip: if your terminal is messed up, try the “reset” command.

## Theory
1. The `file` command.
   `file [option] [file name]` Helps determine the type of a file and its data.
   - To test all files in a folder, the wildcard * can be used. Eg. `file *`
   - The `file` command lets you test a subset of files in a directory using Regex-style ranges.
   - The `file` command lets you use a text file as a list of files to test. Eg. `file -f [filename].txt`. The text file must only contain one file name per line.
   - To test special files, like the system files, use the -s option.
   - To test compressed files, use the -z option.
2. The `find` command.
   Searches for files and directories in a directory hierarchy based on a user given expression and can perform user-specified action on each matched file, like `grep` or `sed`.
   - Find files by name. `find [path_where_to_search] -type f -name document.pdf`
   - Find files by extension. `find [path_where_to_search] -type f -name '*.txt'`
   - Find files by type. `find [path_where_to_search] -type f`. Other file types: -d directory, -f regular file, -l symbolic link, -c character devices, -b block devices, -p named pipe (FIFO), -s socket.
   - Find files by size. `find [path_where_to_search] -type f -size 1024c`. Other suffixes: b: 512-byte blocks (default), c: bytes, w: two-byte words, k: Kilobytes, M: Megabytes, G: Gigabytes.
   - Other criterias include, modification time, owner, permissions.
   
## Solution
1. Login to bandit4.
2. Change the directory with `cd inhere`.
3. When you `ls` into this directory, you get
```
bandit4@bandit:~/inhere$ ls
-file00  -file01  -file02  -file03  -file04  -file05  -file06  -file07  -file08  -file09
````
4. One of these files contain the password and is the only human-readable file in this directory.
5. Solution using `file` command. Since the file names begin with a '-', we need to use the same technique as before to read them.
6. Use `file` command on all the files to see their type. `file ./*`
```
bandit4@bandit:~/inhere$ file ./*
./-file00: PGP Secret Sub-key -
./-file01: data
./-file02: data
./-file03: data
./-file04: data
./-file05: data
./-file06: data
./-file07: ASCII text
./-file08: data
./-file09: data
```
7. Since only -file07 is in ASCII text. This should contain the password to the next level. Use `cat ./-file07` to read the password.
8. When there are more than a few files to go thorugh, using `grep` will be helpful. Grep command can be used to find or search a regular expression or a string in a text file.
9. Use `file ./* | grep ASCII` to get the same result:
```
bandit4@bandit:~/inhere$ file ./* | grep ASCII
./-file07: ASCII text
```
