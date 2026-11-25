# equals and hashcode

these functions are used to compare if two objects are same or not, they are used in hashing based data structures like hashset, hashmap and hashtable, and also in strings, and java 8 collection and stream apis

the exact code in the .equals() method is :

`
public boolean equals(Object obj){
    return (this==obj);
}
`

that means, it checks if the given object is the same object, or a different one, only if it is the same object, then it will return true, else false.

* == checks if two objects have the same address, so inorder to check if two different objects are same based on their values we cannot use ==
we have to use .equals method, we can write whatever logic we want in this method, but by default this also works like ==

hashcode : this function is used in many hashbased data structures to store the objects, but by default it also sees different addresses and different hashes, but if we want two different objects with same values to be hashed the same value, we have to override it

and in java there is a contract that if equals method is overrided, then hashcode method needs to be overriden as well

so, we can use a hashing function like Objects.hash(id, name) then this generates the hash based on the values of the object, instead of the address, so the hashcode for both the objects will be same if their values are same
