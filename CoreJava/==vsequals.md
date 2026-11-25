# == vs .equals()

String constant pool : before learning the differences between == and .equals(), all objects in java are stored in the heap memory, and inside this heap memory there is a special space called string constant pool, where string literals are stored

**** if we use the new keyword to create a string, then that string will be stored in both the heap memory and the string constant pool, but whyyy???this is to basically save the space, and optimize the memory usage

so each time a string is created with new keyword, new object is created in the heap memory, and if this string is not present in the string constant pool, then it will be stored in the pool, so in future if any object is assined this string without the new keyword, it can reference this location in string constant pool

== : checks if the memory location of two objects is same or not
.equals() : ideally it should check if the values of the object are identical or not, instead of their addresses, but by default if you create a new class of your own, this will work the same as ==, you have to override it based on your member variables

