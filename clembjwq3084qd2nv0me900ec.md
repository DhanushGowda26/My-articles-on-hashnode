# Getting started with java 2.0

### Data Types

Data types are used to specify the type of data that can be stored in a variable or object. Java supports several data types, including primitive data types such as int, float, and double, and non-primitive data types such as arrays and strings. Primitive data types are used to store simple values, while non-primitive data types are used to store complex data structures.

```java
int myInt = 10;
float myFloat = 10.5f;
double myDouble = 10.75;
boolean myBoolean = true;
char myChar = 'a';
String myString = "Hello, World!";
```

### Variables

Variables are used to store values in a program. In Java, variables are declared using a specific data type and can be assigned a value using the equal sign (=) operator.

```java
int number = 10;
float price = 20.5f;
String name = "John";
boolean isReady = true;
```

### Typecasting

Typecasting is the process of converting one data type to another. Java supports two types of typecasting: implicit and explicit. Implicit typecasting is done automatically by the compiler, while explicit typecasting requires the developer to specify the conversion.

```java
double myDouble = 10.5;
int myInt = (int) myDouble;
```

### Scanner Class

The Scanner class is used to read input from the user. It can be used to read different data types, including integers, strings, and floats. To use the Scanner class, you need to create an instance of the Scanner class and use its methods to read input.

```java
Scanner scanner = new Scanner(System.in);
System.out.println("Enter your name:");
String name = scanner.nextLine();
System.out.println("Hello, " + name);
```

### Operators

Operators are used to perform operations on variables and values in a program. Java supports several operators, including arithmetic operators (+, -, \*, /), comparison operators (==, !=, &gt;, &lt;), and logical operators (&&, ||, !)

```java
int x = 10;
int y = 5;
int sum = x + y;
int difference = x - y;
int product = x * y;
int quotient = x / y;
boolean isGreater = x > y;
boolean isEqual = x == y;
```

### If-Else Statements

If-else statements are used to execute code based on a condition. If the condition is true, the code in the if block is executed. If the condition is false, the code in the else block is executed.

```java
int number = 10;
if (number % 2 == 0) {
    System.out.println(number + " is even.");
} else {
    System.out.println(number + " is odd.");
}
```

### If-Else-If Statements

If-else-if statements are used when there are multiple conditions to be checked. The code in the if block is executed if the first condition is true. If the first condition is false, the code in the else-if block is executed. This process continues until a condition is found to be true, or the final else block is executed.

```java
int number = 10;
if (number > 0) {
    System.out.println(number + " is positive.");
} else if (number < 0) {
    System.out.println(number + " is negative.");
} else {
    System.out.println(number + " is zero.");
}
```

### Nested Statements

Nested statements are if statements within if statements. They are used when multiple conditions need to be checked, and each condition has its own set of statements.

```java
int number = 10;
if (number > 0) {
    if (number % 2 == 0) {
        System.out.println(number + " is even and positive.");
    } else {
        System.out.println(number + " is odd and positive.");
    }
} else {
    System.out.println(number + " is not positive.");
}
```