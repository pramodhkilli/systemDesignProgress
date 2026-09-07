# Checksum

checksum is basically used to verify if a data is currupted somehow, during transmission or if someone has deliberately currupted it

basically we use some algorithm, pass our bigger data into the algorithm, it give us a smaller result, and we pass this checksum with the request, in the server side, it receives both the checksum and the data, server again calculates the checksum and see if both the checksum's match or not, if they dont then the data is currupted somehow

there are different ways to calculate checksum

CRC : cyclic Redundancy check, these are kind of fast checks, and used heavily, but the issue with them is anyone can tamper the data and create a checksum for that and pass the data

Cryptographic hashes : we use algorithms like SHA-256, this is a bit harder to crack and the chance of producing checksum is difficult for anyone trying to tamper

HMAC and digital signature : it is kindof how TLS works, so a secret key is shared among the server and client, and only these two knows what the key is, so the chance of tampering data is less, cause no other people have this secret key
