# Storing readable passwords

### Description

We sometimes need to authenticate users tp provide access to their accounts tp prevent privacy breach.

### Why is it bad?

When you store passwords as VARCHAR, you risk exposure as:

* someone using tools such as Wireshark to intercept network packets sent from application to server.
* someone who has access to server logs can read user passwords,etc

### Fix

You could store a 1 way salted hash value in your database. You could read more about what Salt in cryptography means [here](https://en.wikipedia.org/wiki/Salt_%28cryptography%29). You can also check SHA -2 [here](https://en.wikipedia.org/wiki/SHA-2) which is usually used as the 1 way hash function.



