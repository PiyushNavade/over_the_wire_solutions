# [Bandit Level 16 → Level 17](https://overthewire.org/wargames/bandit/bandit17.html)

## Goal
The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range 31000 to 32000. 
First find out which of these ports have a server listening on them. Then find out which of those speak SSL/TLS and which don’t. 
There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.

## Theory - `Nmap`
1. In this task, we have to perform port scanning to find out open ports between port range 31000 to 32000.
2. A port can be seen as an address for a specific service. Every computer has ports with the numbers 0 to 65535.
3. Some services have standard ports, like HTTP/80 or SSH/22.
4. An open port means that the host offers a service to the network on this port.

## Solution
1. Use `nmap -sV localhost -p 31000-32000` to start port scanning. `-sV` flag does a service detection scan which is required here. And `-p` flag defines the port range.
```
PORT      STATE SERVICE     VERSION
31046/tcp open  echo
31518/tcp open  ssl/echo
31691/tcp open  echo
31790/tcp open  ssl/unknown
31960/tcp open  echo
```
2. We find that there are 5 open ports. Only 31518 and 31790 runs ssl. Port 31518 runs an echo service, which basically means that it returns whatever we give it as input.
3. Therefore our port of interest is port number 31790. Now connect to this port using `openssl`, similar to the last level.
```
openssl s_client -connect localhost:31790
```
