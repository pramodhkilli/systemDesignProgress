# TLS

imagine you are sending your username and password of your banking website, this request has to go through many routers to reach the server, anyone in the between can see this information and steal it

how to stop it?? this is where TLS comes in

TLS solves problems related to encryption(no one knows), authenticity(you are sending it to the correct server), and integrity(no tampering of data)

how does TLS achieve this??

first, from server side, server has to apply for the certificate from its domain provider, it will give you the certificate, and also the keys, public and private keys

client then calls the website, website return the certification along with the public key

client then uses this key to encrypt another key(symmetric key) and sends it over to the server, server decrypts it using the private key, so now server has the symmetric key

from here starts the real communication, client then encrypts the data using the symmetric key, and sends the requests, as server has already received the symmetric key, it can use it to decrypt this data

but waitttt, why can't we just use the asymmetric encryption and send the data everytime, what is the need to encrypt a key first and send it to the server and then use symmetric encryption
-> because asymmetric encryption is costly, so we use it only for sending the key
