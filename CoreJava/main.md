# main method

main method is the one that runs when we start a java program

public static void main(String[] args){
    System.out.println ("Hello World");
}

public : public means, we can access the method outside the scope of this class

so what happens is that whenever you try to run a program, the jvm looks for the main method, and calls the main method, so in order for the jvm to access the main method, it has to be public

static : inorder to call the method without creating an object of the class, you need the method to be static

void : it is the return type, we do not expect our method to return anything

String[] args : lets consider the scenario of a command line interface, if you want to give an argument to the script or your application, you have to collect them, so args will collect them and store them, instead of args you can use anything, it is just a argument name, you can name the argument name anything like you can for any other object

you can write multiple main methods by changing the argument type like from String to int, but jvm will only consider thew method with the String as the argument

what happens if we have multiple classes that have main method each????

this is possible, but the thing is that it is like you are creating two different applications, which will be executed when their name is called, there wont be any issue