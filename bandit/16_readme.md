# [Bandit Level 15 → Level 16](https://overthewire.org/wargames/bandit/bandit16.html)

## Goal
The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL/TLS encryption.

## Theory
OpenSSL is a library for secure communication over networks. It implements the Transport Layer Security (TLS) and Secure Sockets Layer (SSL) cryptographic protocols.
`openssl s_client` is the implementation of a simple client that connects to a server using SSL/TLS.

## Solution
1. The task says to give the current password to the service running on port 30001 on localhost. And we have to use SSL/TLS encryption.
2. Therefore we use the `openssl s_client` command to implement a simple client and connect to the service.
```
openssl s_client -connect localhost:30001
```
3. Once prompted enter the current level password.
