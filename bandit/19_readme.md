# [Bandit Level 18 → Level 19](https://overthewire.org/wargames/bandit/bandit19.html)

## Goal
The password for the next level is stored in a file readme in the homedirectory. Unfortunately, someone has modified .bashrc to log you out when you log in with SSH.

## Theory
The `.bashrc` file in Linux is a hidden script file located in a user's home directory. It's executed every time a user opens a new interactive Bash shell session, meaning a new terminal window or tab.
The `.bashrc` file has been edited to log you out as soon as you login with ssh.

`ssh` can be used to not only perform remote login but we can also execute commands while sshing.

## Solution
1. I used `cat` command with `ssh` to read the readme file.
```
root@7516a139be30:/# ssh bandit18@bandit.labs.overthewire.org -p 2220 cat readme
                         _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

bandit18@bandit.labs.overthewire.org's password:
cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8
```
