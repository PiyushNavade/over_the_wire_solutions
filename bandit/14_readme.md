# [Bandit Level 13 → Level 14](https://overthewire.org/wargames/bandit/bandit14.html)

## Goal
The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. For this level, you don’t get the next password,
but you get a private SSH key that can be used to log into the next level. Note: localhost is a hostname that refers to the machine you are working on.

## Theory
1. To login using `ssh` without a password, is to use a ssh key and the `-i` option with the `ssh` command.
2. The public key is placed on the computers that should allow access to the user that owns the private key. 
3. Only the user knows the private key.

## Solution
1. Login to bandit13 and use the `ls` command to see the private ssh key.
```
bandit13@bandit:~$ ls
sshkey.private
```
2. Next step is to copy this sshkey.private on your local machine. To do this, use the `scp` command. The syntax indicates the port to use, the source address and the destination.
```
root@7516a139be30:/# scp -P 2220 bandit13@bandit.labs.overthewire.org:sshkey.private .
                         _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

bandit13@bandit.labs.overthewire.org's password:
sshkey.private                                                                        100% 1679    17.0KB/s   00:00
```
3. Once you have the private key, use `ssh` with the `-i` flag to login to bandit14.
```
root@7516a139be30:/# ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220
```
