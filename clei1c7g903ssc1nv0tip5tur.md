# Getting started with Java

## Hello world program

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, world!");
    }
}
```

* `public`: a keyword that indicates that the following class or method can be accessed from anywhere in the program.
    
* `class`: a keyword that is used to define a new class.
    
* `HelloWorld`: the name of the class we're defining.
    
* `{}`: curly braces are used to define the scope of the class.
    
* `public static void main(String[] args)`: the main method is the entry point of any Java program. It is declared as `public` so that it can be accessed by any class, `static` so that it can be called without an instance of the class(object), `void` since it does not return any value, and `main` is the name of the method. `String[] args` is an array of strings that can be passed as command-line arguments to the program.
    
* `System`: a class in Java that provides access to the system, including input and output streams.
    
* `out`: a static member of the `System` class that represents the standard output stream.
    
* `println`: a method of the `PrintStream` class (which is what `System.out` is) that prints a string to the console and then adds a new line character.
    
* `"Hello, World!"`: the string to be printed to the console. Note that strings in Java are enclosed in double quotes
    

## Internal Workflow

In Java, the process of creating an executable program involves two stages: compilation and runtime execution.

Compilation:

Java code is compiled into bytecode by the Java compiler, which is a program that comes with the Java Development Kit (JDK). Bytecode is a low-level, platform-independent representation of the code that can be executed on any device that has a Java Virtual Machine (JVM) installed.

To compile a Java program, you need to use the `javac` command, followed by the name of the Java source code file. For example, if your file is called [`HelloWorld.java`](http://HelloWorld.java), you would type:

```bash
javac helloworld.java
```

If there are no errors in the code, the compiler will generate a file called `HelloWorld.class`, which contains the bytecode.

Runtime Execution:

Once the bytecode has been generated, it can be executed on any device that has a JVM installed. To run the program, you need to use the `java` command, followed by the name of the class that contains the `main` method. For example, to run the `HelloWorld` program, you would type:

```bash
java HelloWorld
```

This will execute the `main` method in the `HelloWorld` class, which will print the "Hello, world!" message to the console.

During runtime execution, the JVM loads the bytecode into memory and interprets it, executing the instructions one at a time. The JVM also provides features such as garbage collection, which automatically frees up memory that is no longer needed by the program, and security, which protects the program from malicious code

\* The file name and class name should be the same and must save the file with an extension of .java

If you only need to run Java applications, then you can download the JRE package. The JRE package includes the JVM and the class libraries needed to execute Java programs.

If you want to develop Java applications, then you need to download the JDK package. The JDK package includes the JRE, as well as the Java compiler (`javac`), the Java Virtual Machine (JVM), Just In Time (JIT) and various development libraries and utilities needed to develop Java programs.

So, if you download and install the JDK package, you will get the JRE as well as the other development tools. However, if you download and install only the JRE package, you will not have access to the development tools included in the JDK.