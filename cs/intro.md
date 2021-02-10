# SOLID
__SOLID__ is a mnemonic acronym for five design principles inteded to make software designs more understandable, flexible, and maintainable.

## Single Responsability Principle
A class should have one, and only one, reason to change. A class should only have one responsability.

> “When designing our classes, we should aim to put related features together, so whenever they tend to change for the same reason. And we should try to separate features if they will change for different reasons. - Steve Fenton

## Open/Closed Principle
Software entities (classes, modules, functions, etc.) should be open for extension, but closed for modification.

> “Open for extension means that we should be able to add new features or components to the application **without breaking** existing code. Closed for modification means that **we should not introducte breaking changes to existing functionality**, because that would force you to refactor a lot of existing code. – Eric Elliot

In JavaScript, we can achieve this by using **function composition**.

## Liskov Substitution Principle
Objects of a superclass shall be replaceable with objects of its subclasses without breaking the application. An overriden method of a class needs to accepts the same input parameter and return the same return value as the method of the superclass.

## Interface Segregation Principle
Clients should not be forced to depend upon interfaces that they do not use.

## Dependency Inversion Principle
High-level modules should not depend on low-level modules. Both should depend on abstrations. Abstrations should not depend on details. Details should depend on abstractions.

High-level modules, which provide complex logic, should be easily reusable and unaffected by changes in low-level modules, which provide utility features.

We can use *dependency injections* to accomplish this decoupling.

# Object-Oriented Programming (OOP) Concepts
## Java Concepts
### Abstraction
Using simple things to represent complexity. You don't need to know how something works to use it. In Java, objects, classes, and variables represent more complex underlying code and data.

### Encapsulation
The practice of keeping fields within a class private, then providing access to them via public methods. It's a protective barrier that keeps the data and code safe within the class itself.

### Inheritance
You let a new class adopt the properties of another. The inheriting class is usually called subclass or a child class, while the original one parent.

### Polymorphism
Use of the same word to mean different things in different contexts. Classes can be used with the same interface. A class that inherits attributes of another class can be called "polymorphic". Java supports two kinds of polymorphism:
- __Static polymorphism__ → you can overload a method with different sets of parameters. The compiler statically binds the method call to a specific method.
- __Dynamic polymorphism__ → a subclass can override a method of its superclass. If you instantiate the subclass, the JVM will always call the overridden method, even if you cast the subclass to its superclass.

## Composition
It describes a class that references one or more objects of other classes in instances variables. It allows you to reuse code without modeling an is-a association, as you do by using inheritance. In the real world, it's found quite regularly: a car has an engine but it's not one.

## Helper class vs. Utility class
__Helper class__ → used to assist in providing some functionality, which isn't the main goal of the application or class in which it is used.

__Utility class__ → special case in which the methods are all static.

# Imperative vs. Declarative Programming
> “Imperative programming is like how you do something, and declarative programming is more like what you do”

__Imperative programming__ → is concerned with how something is implemented, what are the necessary steps to accomplish something.

__Declarative programming__ → is concerned with what you want to be done. You're describing what you're trying to achieve, without instructing how to do it. Many declarative approaches have some sort of underlying imperative abstraction.

# Keywords
__Deserialization__ → converting a string to a native object.\
__Serialization__ → converting a native object to a string so it can be transmitted across the network.

__MIME type__ (media type or content type) → string sent along with a file indicating the type of the file, *e.g.* `audio/ogg`, `application/json`. It serves the same purpose as filename extensions on Windows.

# Sources
[Stackify](https://stackify.com)\
[SOLID Principles every Developer Should Know – Bits and Pieces](https://blog.bitsrc.io/solid-principles-every-developer-should-know-b3bfa96bb688)\
[S.O.L.I.D The first 5 principles of Object Oriented Design with JavaScript – Medium](https://medium.com/@cramirez92/s-o-l-i-d-the-first-5-priciples-of-object-oriented-design-with-javascript-790f6ac9b9fa)\
[Imperative vs Declarative Programming - U;](https://ui.dev/imperative-vs-declarative-programming/)\
[Helper class - Wikipedia](https://en.wikipedia.org/wiki/Helper_class)
