---
title: "Understanding Classes, Objects, and Constructors in JavaScript"
seoTitle: "JavaScript Classes and Objects: Exploring Fundamentals and Examples"
seoDescription: "Learn the fundamentals of JavaScript classes and objects with examples. Understand the relationship between classes, objects, and constructors."
datePublished: Sun Jun 04 2023 05:00:41 GMT+0000 (Coordinated Universal Time)
cuid: cligyg1gc01bna3nvhzc60yme
slug: understanding-classes-objects-and-constructors-in-javascript
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1685808941801/ea6d2243-ced0-44ab-a7e3-88c3d2a4558e.png
tags: javascript, web-development, webdev, functional-programming, oops

---

## Class and Object

In JavaScript, a class is a blueprint or a template for creating objects with similar properties and methods. It defines the structure and behavior that objects of that class should have. Think of a class as a blueprint for creating multiple instances of the same type of object.

```javascript
class Car {
  constructor(make, model) {
    this.make = make;
    this.model = model;
  }

  start() {
    console.log(`The {this.make} {this.model} is starting...`);
  }

  drive(speed) {
    console.log(`Driving the {this.make} ${this.model} at {speed} mph.`);
  }
}
```

In this example, we define a "Car" class using the "class" keyword. The class has a constructor method, which is called when an object is created from the class. It takes parameters ("make" and "model") and assigns them to the object's properties ("this.make" and "this.model").

The class also has two methods: "start" and "drive". The "start" method logs a message indicating that the car is starting, and the "drive" method logs a message indicating the speed at which the car is being driven.

Now that we have the class blueprint, we can create instances of car objects based on this class.

```javascript
const car1 = new Car("Tesla", "Model S");
const car2 = new Car("Toyota", "Camry");

car1.start(); // Output: The Tesla Model S is starting...
car2.drive(60); // Output: Driving the Toyota Camry at 60 mph.
```

In this example, we create two car objects, "car1" and "car2", using the "new" keyword followed by the class name and passing the necessary arguments. Each car object created has its own set of properties ("make" and "model") with the values provided.

We can then call the methods defined in the class on these objects. For example, calling "car1.start()" invokes the "start" method specific to "car1", and calling "[car2.drive](http://car2.drive)(60)" invokes the "drive" method specific to "car2" with a speed argument of 60.

By using classes, we can easily create objects with consistent properties and behaviors. It promotes code reusability and helps in organizing and structuring our code.

## Functions v/s Methods v/s Constructors

1. Functions: A function in JavaScript is a reusable block of code that performs a specific task. It allows you to organize and modularize your code by encapsulating a set of instructions. Functions can be invoked and executed multiple times throughout your code.
    

```javascript
// Example 1: Addition function
function add(a, b) {
  return a + b;
}

console.log(add(2, 3)); // Output: 5

// Example 2: Greeting function
function greet(name) {
  console.log(`Hello, {name}!`);
}

greet("John"); // Output: Hello, John!
```

In the first example, the `add` function takes two parameters `a` and `b` and returns their sum. It can be called with arguments `2` and `3`, resulting in the output `5`.

The second example defines a `greet` function that takes a `name` parameter and logs a greeting message. By calling `greet("John")`, it outputs "Hello, John!".

1. Methods: A method is a function that is associated with an object or a class. It operates on the data or properties of that object and can be called using the object's name, followed by a dot notation.
    

```javascript
// Example 1: Array method
const numbers = [1, 2, 3, 4, 5];

console.log(numbers.length); // Output: 5

// Example 2: String method
const message = "Hello, World!";

console.log(message.toUpperCase()); // Output: HELLO, WORLD!
```

In the first example, `length` is a method associated with the `numbers` array object. It returns the number of elements in the array when called as `numbers.length`.

The second example utilizes the `toUpperCase` method of the `message` string object. It converts the string to uppercase letters when called as `message.toUpperCase()`.

1. Constructors: A constructor is a special type of function used to create and initialize objects from a class blueprint. It sets up the initial state of the object by defining properties and assigning values.
    

```javascript
// Example 1: Person constructor
function Person(name, age) {
  this.name = name;
  this.age = age;
}

const person1 = new Person("John Doe", 30);
console.log(person1); // Output: { name: 'John Doe', age: 30 }

// Example 2: Car constructor
function Car(make, model) {
  this.make = make;
  this.model = model;
}

const car1 = new Car("Tesla", "Model S");
console.log(car1); // Output: { make: 'Tesla', model: 'Model S' }
```

In the first example, we define a `Person` constructor function that takes `name` and `age` parameters. Inside the constructor, [`this.name`](http://this.name) and `this.age` assign the parameter values to the properties of the object being created. By using `new Person("John Doe", 30)`, we create an instance of the `Person` object with the provided values.

Similarly, in the second example, the `Car` constructor assigns the `make` and `model` parameters to the corresponding properties of the object being created. With `new Car("Tesla", "Model S")`, we create a `car1` object with the specified make and model values.

In summary, functions are reusable blocks of code, methods are functions associated with objects or classes, and constructors are special functions used to construct and initialize objects from a class blueprint.

## Object Constructor

Using an Object Constructor: JavaScript allows us to define custom object types using constructor functions. A constructor function serves as a blueprint for creating multiple objects with similar properties and methods using the `new` keyword.

```javascript
// Custom constructor function for creating a person object
function Person(name, age) {
  this.name = name;
  this.age = age;
  this.greet = function() {
    console.log(`Hello, my name is {this.name} and I'm {this.age} years old.`);
  };
}

// Creating a person object using the constructor
const person1 = new Person("John Doe", 30);
const person2 = new Person("Jane Smith", 25);

person1.greet(); // Output: Hello, my name is John Doe and I'm 30 years old.
person2.greet(); // Output: Hello, my name is Jane Smith and I'm 25 years old.
```

In this example, we define a `Person` constructor function that takes `name` and `age` parameters. Inside the constructor, we use the `this` keyword to refer to the newly created object. We assign the `name` and `age` values to the respective properties of the object. Additionally, we define a `greet` method that logs a greeting message using the object's `name` and `age` properties.

By using the `new` keyword followed by the constructor function, we can create multiple instances of the `Person` object, such as `person1` and `person2`. Each instance has its own set of properties and methods.

```javascript
// Custom constructor function for creating a car object
function Car(make, model, year) {
  this.make = make;
  this.model = model;
  this.year = year;
  this.start = function() {
    console.log(`The {this.make} {this.model} is starting...`);
  };
}

// Creating a car object using the constructor
const car1 = new Car("Tesla", "Model S", 2023);
const car2 = new Car("Toyota", "Camry", 2022);

car1.start(); // Output: The Tesla Model S is starting...
car2.start(); // Output: The Toyota Camry is starting...
```

In this example, we create a `Car` constructor function that takes `make`, `model`, and `year` parameters. Inside the constructor, we assign the parameter values to the corresponding properties of the object using the `this` keyword. We also define a `start` method that logs a message indicating the car is starting.

`this` Keyword: In JavaScript, the `this` keyword refers to the context in which a function is executed. It allows us to access and manipulate properties and methods within an object.

In the context of object constructors, the `this` keyword refers to the object being created or instantiated. It allows us to assign values to properties and define methods specific to each instance of the object.

For example, in the `Person` constructor function, when we use [`this.name`](http://this.name) `= name`, we are assigning the `name` parameter value to the `name` property of the newly created person object.

Similarly, in the `greet` method of the `Person` constructor, [`this.name`](http://this.name) and `this.age` refer to the `name` and `age` properties of the object that called the `greet`

**If you find value in this content, don't forget to like and comment on the blog post. Feel free to follow me on** [**Twitter**](https://twitter.com/dhanuks26)**,** [**GitHub**](https://github.com/DhanushGowda26)**, and** [**Hashnode**](https://dhanushks.hashnode.dev/) **for more valuable content. Stay tuned for future articles where we explore more such content.**

**Thank you for reading! 🙏 Your time and attention are greatly appreciated! If you have any further questions or need additional information, please don't hesitate to ask. 😊**