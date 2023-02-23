# Basic Terms before getting into
Programming

### Compile time:

Compile time refers to the period during which the source code of a program is compiled into executable code. This includes syntax checking, type checking, and optimization of the code. Errors and warnings discovered during compilation need to be fixed before the code can be executed. The compile time is performed once before the code is executed.

### Run time:

Run time refers to the period during which the program is actually executed. This includes input/output operations, memory allocation, and processing of the code. Errors that occur during runtime may cause the program to terminate abruptly or produce incorrect output.

### Execution time:

Execution time refers to the total amount of time required to execute a program. It includes both the compile time and the run time. The execution time depends on the complexity of the program, the efficiency of the algorithm, and the performance of the hardware.

In summary, compile time is the time taken to convert the source code into an executable format, run time is the time taken to execute the program, and execution time is the total time taken to compile and run the program

### Static Language:

A static language is a programming language in which variable types are determined at compile time. This means that the types of variables must be declared explicitly in the source code, and the compiler checks that the types match the operations performed on them. Examples of static languages include Java, C, C++, and Go.

In contrast, a dynamic language is a programming language in which variable types are determined at runtime. This means that variables can have different types during execution, and type checking is performed during runtime. Examples of dynamic languages include Python, Ruby, JavaScript, and PHP.

Here is an example of a static language (Java) and a dynamic language (Python):

Java (static language):

```java
public class Example {
  public static void main(String[] args) {
    int x = 10;
    String str = "Hello, world!";
    System.out.println(str + x);
  }
}
```

In this example, `int` and `String` is explicitly declared as variable types, and the compiler checks that the `+` operator is used only on variables of the same type.

### Dynamic Language:

```python
x = 10
str = "Hello, world!"
print(str + str(x))
```

In this example, variable types are not explicitly declared, and the type of `x` is determined at runtime when `str(x)` is executed. Type checking is performed during runtime, and the code will raise a `TypeError` if the types are not compatible.

Both static and dynamic languages have their advantages and disadvantages, and which one to choose depends on the specific needs of the project.

### Memory

In computer programming, stack and heap are two different types of memory storage areas that are used to manage and store data and instructions during program execution.

1. Stack Memory: The stack is a portion of memory that is used to store temporary data created by a function or a block of code. It is a contiguous block of memory that is managed by the computer's operating system. The stack is a Last-In-First-Out (LIFO) data structure, meaning that the last item pushed onto the stack is the first item that will be popped off the stack.
    

In most programming languages, when a function is called, a block of memory is reserved on the stack for the function's local variables, parameters, and return address. When the function returns, the memory used by the function is released from the stack. This makes the stack memory very efficient, as the operating system doesn't have to manage it explicitly.

1. Heap Memory: The heap is a section of memory used to store dynamically allocated data. Unlike the stack, the heap is not managed automatically by the operating system. Instead, the programmer must explicitly allocate and deallocate memory on the heap.
    

When memory is allocated on the heap, the operating system finds a block of memory that is large enough to hold the requested amount of memory and marks it as allocated. When the memory is no longer needed, it must be explicitly deallocated by the programmer. If memory is not deallocated, it can lead to memory leaks, where memory is tied up indefinitely and can cause the program to run out of memory.

The heap is a much larger memory area than the stack, and it allows for dynamic allocation of memory at runtime. This makes it a powerful tool for programming complex data structures like linked lists, trees, and graphs.

In summary, the stack and the heap are two different memory areas used by computer programs. The stack is used to store temporary data created by a function or a block of code, while the heap is used to store dynamically allocated data. Understanding the difference between stack and heap memory is important for writing efficient and bug-free code.

example:

```python
    # integer object is created and its reference is stored on the stack
    x = 42  
    # list object is created and its reference is also stored on the stack
    y = [1, 2, 3]  
    # string object is created and its reference is stored on the heap
    z = "hello world"
```

In this example, `x` and `y` are stored on the stack, while the `int` object 42, `list` object `[1, 2, 3]` and the `string` object `"hello world"` are stored on the heap.

### Reference Variable and Object

A reference variable is a type of variable that holds the memory address of another object or variable. Instead of storing the actual value, a reference variable holds a reference or pointer to the memory location where the object or variable is stored.

An object, on the other hand, is an instance of a class in object-oriented programming. An object is created from a class and contains both data and methods that operate on that data. Objects are a fundamental concept in object-oriented programming and are used to represent real-world entities or concepts in software.

Together, reference variables and objects are used to manage memory and allow for complex data structures to be created and manipulated in programming languages that support them.

Reference variables and objects are stored in stack and heap memory respectively.

If the object was changed via one reference variable then this change applies to all the reference variables pointing towards the same object.

Example:

Here 'a' and 'b' are reference variables and '10' is an object.

Initially 'a' is assigned as '10' and 'b' is assigned as 'a' and by changing 'a' to let's say '100' and printing 'b' what do you expect 'b' to be '10' or '100' comment down.

\*Class and object, Local and Global Variable and much more terms that you will learn while learning a particular programming language but as of now you know the terminologies required to get started with programming.