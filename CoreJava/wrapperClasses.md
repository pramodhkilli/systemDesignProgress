# wrapper classes

Java is not 100% object oriented language, because java has primitive data types like int, bool, short, float which are not objects

but in order to use these data types with in java, we have to somehow make them into objects, otherwise the collections framework or any other data structure does not work, here comes the wrapper classes like Integer, Boolean, Short, Float, Character

basically, they are just classes with a single member variable which is a primitive type, but this opens up a new world for them

the methods like toString, Integer.valueOf, Integer.parseInt, Integer.MIN_VALUE, Integer.MAX_VALUE, integer.max(), Integer.min(), and many more

boxing : manually wrapping a primitive type to make a wrapper object, Integer a = Integer.valueOf(10)
autoBoxing : automatically wrapping a primitive type, Integer a = 10
unboxing : manually unwrapping a wrapper object to make a primitive type, int x = Integer.parseInt(a)
autoUnboxing : automatically unwrapping a wrapper object, int x = a
