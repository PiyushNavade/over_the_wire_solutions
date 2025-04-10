# [Bandit Level 0 → Level 1](https://overthewire.org/wargames/bandit/bandit1.html)

## Goal
The password for the next level is stored in a file called readme located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game.

## Theory
1. The `ssh` command.
   `ssh [options] username@hostname`
   `ssh` command connects and logs into the specified hostname or username. The user must prove their identity, through password or a ssh key, to the remote machine to establish a connection.
   - -p - to specify the port number.
   - -i - to login with a sshkey.
   - `ssh-keygen -t rsa` - to generate a public-private key pair.
   - `ssh-copy-id [hostname_OR_ip]` - to copy the public key to the server.
   - SCP is a reliable tool for securely transferring files over the SSH protocol.
      `scp [file_name] [username]@[remotehost_OR_ip]:[port]/home/username/destination`
2. The `ls` command.
   `ls` command is used to list files and directories within the file system. Some useful options:
   - -a - to include hidden files.
   - -l - to descriptively list the files and directories.
   - -h - human-readable.
   - -S - sort by size, largest first.
   - -t - sort by modification time, newest first.
5. The `cat` command.
   `cat` command displays file contents. It reads one or multiple files and prints their content to the terminal. `cat` is used to view file contents, combine files, and create new files.
   - `cat >[filename]` - creates a file.
   - `cat [file1] > [file2]` - copies content of file1 to file2, overwriting file2.
   - `cat [file1] >> [file2]` - appends content of file1 to file2.
   
## Solution
1. To login as bandit0 using ssh on port 2220 use `ssh bandit0@bandit.labs.overthewire.org -p 2220`. At the prompt, enter bandit0 as the password.
2. We are now logged in as bandit0. The password for the next level is located in a file called **readme**.
3. The command `ls` does the trick here. Theres only one file located in the home directory of bandit0.
4. Just read the file using `cat readme` and get the password.
