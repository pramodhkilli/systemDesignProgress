# why strings are immutable in java

once we assign a string a value, it will be stored in the string constant pool, if we now change the value, then a new string is added to the pool if not present already and the variable will point to this string now, so the first string will remain as it is in the string constant pool

lets consider this example

string s1 = "Hello"
string s2 = s1 + "World"

so here s1+"world" give a new object, not a string literal, so this will be stored in the heap memory, and in our string constant pool, we have the string hello and world

+ here is kind off like a function that returns a new object, so it kindoff stores the new string in the heap memory
