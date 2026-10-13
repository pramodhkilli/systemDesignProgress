# Bloom Filters

Lets consider a situation, i am creating an instagram account, which already has billions of users, i have to enter a unique user name, for that instagram need to check my entered username is available in db or not, if it is already present, i have to choose another, if not i can take that

Lets say instagram has 1B users, even after indexing, i have to query the DB for a username, multiple times for a single users(considering that the entered user name is already taken 2-3 times)

and at a moment there could be many people trying to create an account, this increases the load on that DB, so how will you as an engineer solve this issue

the naive thought that comes to mind is use a seperate storage that is easy and faster to access like a hashmap, so every time an api call comes, i will do the task in O(1) time, and return the value, but the issue is that at 1B scale storing something in server or even cache for billion users apart from the other mandatory caching is a headache

there should be some other way, this is where bloom filters comes into picture

consider a large bit array of size m, and there are K hash functions, each time a username is registered or created an account, i will enter the details of that username into this array

step 1: pass the username through K hash function, you will get K results
step 2: mod the k results with M, which makes us able to map the results with our array
step 3: set the bits at these k places

done, when next time a new request comes with this name, we will come to our array, and do the hashing and see if all the bits are set

there could be 2 cases :

case 1: atleast one bit is not set, that means this username is not present and the user can use this, but how can you say that for sure???? if it is already present all the bits should be 1

case 2: all the bits are set, this is the case we consider a false positive, by logic of the case 1 you may think that if all the bits are set, this username is already present and not available for our user, butttttttt what if it is not??? lets say there are two usernames that registered whose modded hash values are 1, 3, 5, 7 and 2, 4, 6, 8. and a new request comes whose modded hash comes out to be 1, 2, 3, 4. all the bits are set from the already existing ones, so we might think that this new username already exists but in reality it does not

so this is a false positive

and to further improve the performance or optimize your bloom filter such that there are less errors we can have multiple layers of bloom filters with different set of hash functions, or we can tweak or play with number of hash functions and the bit array length

one interesting error rate calculation that I learnt from a youtube video by gaurav sen is

1. the probability of a bit being set to 1 from a single hash function is 1/m
2. the probability of a bit remaining same or 0 is 1-(1/m)
3. the probability of a bit to remain 0 after k has functions, that mean for a single string is (1-(1/m))^k
4. for i strings this probability becomes (1-(1/m))^(k*i)
5. so what would be the probability of a bit becomes 1 after i strings ??? 1-(1-(1/m))^(k*i)
6. now the important part, for a string to give false positive, all the bits should be set to 1, so the probability that all the particular bits for the new string to be set to 1 is (1-(1-(1/m))^(k*i))^k
i mean there are k bits that we would get from this string because there are k hash functions, these k bits should be 1

now based on your k values or m values, you can tweak or play on the error rates, or do an integral of this expression to get the maxima and minima
