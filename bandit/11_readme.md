# [Bandit Level 10 → Level 11](https://overthewire.org/wargames/bandit/bandit11.html)

## Goal
The password for the next level is stored in the file data.txt, which contains base64 encoded data.

## Theory
Base64 is a binary-to-text encoding scheme. It can often be recognised by equal signs at the end of the data. However, this is not always the case.

## Solution
1. The file data.txt contains the password which is encoded with base64.
```
bandit10@bandit:~$ cat data.txt
VGhlIHBhc3N3b3JkIGlzIGR0UjE3M2ZaS2IwUlJzREZTR3NnMlJXbnBOVmozcVJyCg==
```
2. Decode using `openssl`
```
openssl enc -base64 -d <<< VGhlIHBhc3N3b3JkIGlzIGR0UjE3M2ZaS2IwUlJzREZTR3NnMlJXbnBOVmozcVJyCg==
```
2. Using the base64 program from the coreutils package.
```
echo VGhlIHBhc3N3b3JkIGlzIGR0UjE3M2ZaS2IwUlJzREZTR3NnMlJXbnBOVmozcVJyCg== | base64 --decode
```
