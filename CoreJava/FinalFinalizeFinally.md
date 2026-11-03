# final finally finalize

1. final :
    1. variable : if a variable is stated as final, then once it is assigned, you cannot change it later, how can we initialize it??? first we can assign the value during declaration, second is we can use a constructor with this final variable as argument and initiaze inside the constructor

    2. method : if a method is declared as final, the child classes cannot override this method

    3. class : if a class is declared as final, then no other class can inherit this class

    important point to note is the syntax is you have to write final before the return type in case of method, and before the data type in case of variable, and after public in case of class

2. finally :
    this is used while doing exception handling, with the try catch block we use finally, if we want to run a piece of code no matter the exception, so before return statement the code inside finally block is executed and then the return statement runs

    this helps when we opened a file in our code and some exception happened, we have to close it no matter what, similarly if you have opened a session in the DB, and some query caused an exception, but you want to close it no matter what

3. finalize :
    finalize is the method which is called at the time of garbage collection by JVM, garbage collection is the process where JVM frees up the memory by deleting all the unreferenced objects.

    finalize method is a part of object class, object class is the parent class of all the classes in java, and after java 8 this method has been deprecated in java
