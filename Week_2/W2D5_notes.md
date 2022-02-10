# Object Oriented Programming 

## Part 1: Classes & Instances



The blueprints is a template for creating a new house, which it has all the details and instrciotns needed to build a house, but each house that is built from the blueprint is different. 

In OOP, classes are templates that we use to create instances of objects. A class describes what the object is going to be and we can create new objects using the class. 

### `Class`

**Classes are blueprints**

to declare a class, you use the `class` keyword with the name or the class

```javascript 
class Pizza {

  // to create new objects from class
  let pizza1 = new Pizza();
  let pizza2 = new Pizza();

}
```
When you create an object using class, you are creating an instance of that class. **pizza1** and **pizza2** are instances of the Pizza class.

though they are created from the same class... 
```javascript
pizza1 === pizza2; // false
```


**Methods and Properties**

to add properties to a class, simply use the `this` keyword followed by the property name, then assign it a value:

```javascript
class SomeClass {

  someMethod() {

    this.hello = 'hi'; // created a property called hello

  };
};
```

**Introduction to `constructor`**

constructor is a special kind of method that gets executed when an object instance is created from a class. The constructor is for setting default valuesfor any new object's properties. 

**Customizing the constructor**

Every class can have a single constructor method that will get called when an instance of that class is created 
```javascript
class Pizza {

  constructor(size, crust) {
    this.size = size;
    this.crust = crust;
    this.toppings = ["cheese"];
  }

  addTopping(topping) {
    this.toppings.push(topping);
  }

}
```
Now every time we use this class to create a new object, we can pass in a size and crust.
```javascript
let pizza3 = new Pizza('large', 'thin');
```

## Primitive as Objects 

an object constructor can be invoked with the word `new`. When we use the object constructor to create a primitive, we run into issues when we try to cpmpare two different strirngs, for instance.

```javascript

const greeting = "Hello, world!" 
const objGreeting = new String("Hello, world!");

greeting == objGreeting; 
// => true

greeting === objGreeting; 
// => false

```
The primitive string is not the exact sae as an object string. To avoid this, we generally do not use object constructors when creating primitives, but object constructors are extremely useful for instantiating the complex objects.


----------


## Part 2: Inheritance

As we start to create different types of objects, inevitably we start to notice some code duplication.
  * constructor 
  * methods


### A solution with `Inheritance`

Moving the shared code from two classes into another class, which the technique is called `inheritance`. 

```javascript
// This class represents all that is common between Student and Mentor
class Person {
  
  constructor(name, quirkyFact) {
    this.name = name;
    this.quirkyFact = quirkyFact;
  }

  bio() {
    return `My name is ${this.name} and here's my quirky fact: ${this.quirkyFact}`;
  }
}
```
```javascript
class Student extends Person {
  // stays in Student class since it's specific to students only
  enroll(cohort) {
    this.cohort = cohort;
  }
}

class Mentor extends Person {
  // specific to mentors
  goOnShift() {
    this.onShift = true;
  }

  // specific to mentors
  goOffShift() {
    this.onShift = false;
  }
}
```

----------

## Part 3: Super

### **Method Overriding and Super**

### `Method Override`

```javascript
// Superclass
class Person {
  constructor(name, quirkyFact) {
    this.name = name;
    this.quirkyFact = quirkyFact;
  }

  bio() {
    return `My name is ${this.name} and here's my quirky fact: ${this.quirkyFact}`;
  }
}

// Subclass
class Mentor extends Person {
  // Completely re-define the bio method since it has more to say
  bio() {
    return `I'm a mentor at Lighthouse Labs. My name is ${this.name} and here's my quirky fact: ${this.quirkyFact}`;
  }
}

// The Student class doesn't need to define bio since it can just use the one from Person

// DRIVER CODE

const bob = new Mentor('Bob Ross', 'I like mountains way too much');
console.log(bob.bio());
```

### `Super`
OOP languages allow subclasses to have a reference on the parent class. This is usually done via the `super` keyword

```javascript 
// Super class
class Person {
  constructor(name, quirkyFact) {
    this.name = name;
    this.quirkyFact = quirkyFact;
  }

  bio() {
    return `My name is ${this.name} and here's my quirky fact: ${this.quirkyFact}`;
  }
}

class Mentor extends Person {
  // Mentor bios need to include a bit more info
  bio() {
    return `I'm a mentor at Lighthouse Labs. ${super.bio()}`;
  }
}

// DRIVER CODE

const bob = new Mentor('Bob Ross', 'I like mountains way too much');
console.log(bob.bio());
```
Using `super` allows us to access the superclass. 

-----

## Part 4: Getters and Setters 

### `Getters` and  `Setters`

```javascript
class Pizza {

  // ... CODE FROM PART 1 ...

  setSize(size) {
    this.size = size;
  }
  getSize() {
    return this.size;
  }
}

// DRIVER CODE
const pizza = new Pizza();
pizza.setSize('m');
pizza.getSize(); // m
```
Two main reasons for using getter and settter: 
1. `Validating data` before assinging it to a property
2. `Computing a value on the fly` instead of simply pulling it out of a property

#### **Validating Data**
Using a setter method instad of setting the property directly, we can have the object validate the value before it gets set. 

#### **Computed Value**
We can compute the value only when it is needed, and not have to constantly update it 


### A better way! `get` and `set`

getter and setter specifically for Javascript 

```javascript
class Pizza {

  // ...

  // replace our custom getters / setters with these ones!
  get price() {
    const basePrice = 10;
    const toppingPrice = 2;
    return basePrice + this.toppings.length * toppingPrice;
  }

  set size(size) {
    if (size === 's' || size === 'm' || size === 'l') {
      this._size = size;
    }
  }
}
```
```javascript
let pizza = new Pizza();

pizza.price;      // instead of getPrice()
pizza.size = 's'; // instead of setSize(size)
```
--------

## OOP Best Practices 

Primary Goals of OOP:
1. Reduce duplicated code (reusability)
2. Breaking code up into sensibly-divided units (modularity)

ultimately it's about trying to make complex things simpler to read, write and maintain. 


