# comparator and comparable

lets consider a list of numbers, if you sort it it will be sorted in ascending order or descending order, now consider an object like employee, which has member variables like id, name and age, how does the sorting logic should behave, should it sort based on id or name or age??

comparable and comparator both are interfaces that allow you to define the logic for comparing two objects, but both of them have their own distinct way of achieving this

comparison logic if a class implements the comparable interface

eg : e1.compareTo(e2);

if the method returns +ve value then e1>e2
if the method returns 0 then e1=e2
if the method returns -ve value then e1<e2

comparator is a functional interface which means it has only i method which does not have a implementation, remaining methods will have the implementation

so the function name is compare( T a, T b);

this accepts two inputs, and you kind of use your implementation of how you would compare based on you need

ex :

Collections.sort(employees,(a,b) -> {
    your sorting logic here, the rules are same as that of comparable
})

the advantage with comparator is you can have multiple sorting functionalities, but with comparable you have to override the method and which can only have one logic for sorting