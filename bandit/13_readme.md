# [Bandit Level 12 → Level 13](https://overthewire.org/wargames/bandit/bandit13.html)

## Goal
The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work.
Use mkdir with a hard to guess directory name. Or better, use the command “mktemp -d”. Then copy the datafile using cp, and rename it using mv (read the manpages!)

## Theory
Some useful commands for this task.
1. `mktemp -d` create a temporary directory inside `/tmp/`.
2. `cp [source] [destination]` copy file.
3. `mv [source] [destination]` move file.

### Hexdumps
1. Hexdumps are often used when we want to look at data that cannot be represented in strings and therefore is not readable, so it is easier to look at the hex values.
2. A hexdump has three main columns. The first shows the address, the second the hex representation of the data on that address and the last shows the actual data as strings.
3. To create a hexdump of a file, use: `xxd [input_file] [output_file]`. With the `-r` flag, it reverts the hexdump.

### [File Signatures](https://en.wikipedia.org/wiki/List_of_file_signatures)
1. Each file type has a magic number/file signature.

### Compression
Compression is a method of encoding that aims to reduce the original size of a file without losing information (or only losing as little as possible). Useful compression types:
1. `gzip` is a command to compress or decompress (-d) files. A ‘gzip’ file generally ends with .gz.
2. `bzip2` is another command which allows for compressing and decompressing (-d) files. A ‘bzip2’ file generally ends with .bz2.
3. `tar` is a command that creates archive files (-cf). It also allows extracting these files again (-xf). A tar archive generally ends with .tar.

## Solution
1. Create a temporary folder.
```
bandit12@bandit:/$ mktemp -d
/tmp/tmp.JjzoWk7c5D
```
2. Copy and remane the data.txt to hexdump and place it in the temporary folder.
```
bandit12@bandit:~$ cp data.txt /tmp/tmp.JjzoWk7c5D
bandit12@bandit:~$ cd /tmp/tmp.JjzoWk7c5D
bandit12@bandit:/tmp/tmp.JjzoWk7c5D$ mv data.txt hexdump_data
bandit12@bandit:/tmp/tmp.JjzoWk7c5D$ ls
hexdump_data
```
3. Since this is a hexdump, according to the task, we will first revert it using:
```
xxd -r hexdump_data compressed_data
```
4. We now need to decompress the data. To figure out what decompression we need to use `xxd`, look at the first bytes in the hexdump to find the file signature.
```
bandit12@bandit:/tmp/tmp.JjzoWk7c5D$ xxd hexdump_data | head
00000000: 1f8b 0808 41d4 f767 0203 6461 7461 322e  ....A..g..data2.
00000010: 6269 6e00 0149 02b6 fd42 5a68 3931 4159  bin..I...BZh91AY
00000020: 2653 59a8 ffa7 8f00 001d 7fff dbeb 7ffa  &SY.............
```
5. The first bytes of the file are `\x1F\x8B`, therefore it is a gzip compressed file. To decompress it, first rename it with .gz.
```
bandit12@bandit:/tmp/tmp.JjzoWk7c5D$ mv compressed_data compressed_data.gz
bandit12@bandit:/tmp/tmp.JjzoWk7c5D$ gzip -d compressed_data.gz
```
6. The resulting file is still compressed. Using `xxd` again, find the file signature.
```
bandit12@bandit:/tmp/tmp.JjzoWk7c5D$ xxd compressed_data
00000000: 425a 6839 3141 5926 5359 a8ff a78f 0000  BZh91AY&SY......
00000010: 1d7f ffdb eb7f fabb 7fa5 efbb 7ef5 fbfd  ............~...
```
7. The first bytes of the file are `\x42\x5a\x68`, therefore it is a bzip2 compressed file. To decompress it, first rename it with .bz2.
```
bandit12@bandit:/tmp/tmp.JjzoWk7c5D$ mv compressed_data compressed_data.bz2
bandit12@bandit:/tmp/tmp.JjzoWk7c5D$ bzip2 -d compressed_data.bz2
bandit12@bandit:/tmp/tmp.JjzoWk7c5D$ xxd compressed_data | head
00000000: 1f8b 0808 41d4 f767 0203 6461 7461 342e  ....A..g..data4.
00000010: 6269 6e00 edd1 4b48 9461 1480 e14f c469  bin...KH.a...O.i
```
8. The resulting file is still not fully decompressed. And now it is gzip.
```
bandit12@bandit:/tmp/tmp.JjzoWk7c5D$ mv compressed_data compressed_data.gz
bandit12@bandit:/tmp/tmp.JjzoWk7c5D$ gzip -d compressed_data.gz
bandit12@bandit:/tmp/tmp.JjzoWk7c5D$ xxd compressed_data | head
00000000: 6461 7461 352e 6269 6e00 0000 0000 0000  data5.bin.......
00000010: 0000 0000 0000 0000 0000 0000 0000 0000  ................
```
9. The newly decompressed file has `\x64\x61\x74` as the starting bytes, therefore now we have an archieve. Use `tar` to extract the file.
```
andit12@bandit:/tmp/tmp.W5t1vua6G9$ mv compressed_data compressed_data.tar
bandit12@bandit:/tmp/tmp.W5t1vua6G9$ tar -xf compressed_data.tar 
bandit12@bandit:/tmp/tmp.W5t1vua6G9$ ls
compressed_data.tar  data5.bin  hexdump_data
```
10. Here we see that `data5.bin` appears in our directory.
```
bandit12@bandit:/tmp/tmp.JjzoWk7c5D$ xxd data5.bin | head
00000000: 6461 7461 362e 6269 6e00 0000 0000 0000  data6.bin.......
```
11. `data5.bin` is another archieve which contains `data6.bin`. Extract it.
```
bandit12@bandit:/tmp/tmp.JjzoWk7c5D$ tar -xf data5.bin
bandit12@bandit:/tmp/tmp.JjzoWk7c5D$ ls
compressed_data.tar  data5.bin  data6.bin  hexdump.gz
bandit12@bandit:/tmp/tmp.JjzoWk7c5D$ xxd data6.bin | head
00000000: 425a 6839 3141 5926 5359 9e50 1aa4 0000  BZh91AY&SY.P....
```
12. Now we again have a file, `data6.bin`, which seems to be compressed using bzip2.
```
bandit12@bandit:/tmp/tmp.W5t1vua6G9$ bzip2 -d data6.bin
bzip2: Can't guess original name for data6.bin -- using data6.bin.out
bandit12@bandit:/tmp/tmp.W5t1vua6G9$ ls
compressed_data.tar  data5.bin  data6.bin.out  hexdump_data
```
13. `data6.bin.out` shows another file name `data8.bin` again. So we extract this file.
```
bandit12@bandit:/tmp/tmp.W5t1vua6G9$ tar -xf data6.bin.out
```
14. This file, `data8.bin`, is gzip and decompressing it once again gives us the password.
```
bandit12@bandit:/tmp/tmp.W5t1vua6G9$ xxd data8.bin | head
00000000: 1f8b 0808 0650 b45e 0203 6461 7461 392e  .....P.^..data9.
bandit12@bandit:/tmp/tmp.W5t1vua6G9$ mv data8.bin data8.gz
bandit12@bandit:/tmp/tmp.W5t1vua6G9$ gzip -d data8.gz
bandit12@bandit:/tmp/tmp.W5t1vua6G9$ ls
compressed_data.tar  data5.bin  data6.bin.out  data8  hexdump_data
bandit12@bandit:/tmp/tmp.W5t1vua6G9$ cat data8
The password is 8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL
```
