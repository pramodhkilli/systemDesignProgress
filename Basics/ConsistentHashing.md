Problem statement : 
    Lets say you have a architecture, that has multiple services, or you have a architecture that has multiple data base partitions, how to figure out which server the request should go?

Consistent hashing :
    we pass the server id's through hash function, and get some number, and same thing we do with some userId or request specific unique identifier, with the same hash, or different hash function, and see which server's hash is the first greater than the request's hash

    example : you have 4 servers
        hash of those 4 servers is 14, 22, 70, 54

        now let's arrange these in ascending order, 14, 22, 54, 70
        now compute the hash for the request : 36

        so the first value that is greater than 36 is 54, so the request goes to the server whose hash value is 54

    now to reduce the skew, in our case 14 is near to 22, but 54 is far from 70, we can use multiple hash functions, which generate different values for the same server id, this way we will have more values, and we can route the requests accordingly