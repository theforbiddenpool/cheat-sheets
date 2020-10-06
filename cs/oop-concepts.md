# Java Concepts
## Abstraction
Using simple things to represent complexity. You don't need to know how something works to use it. In Java, objects, classes, and variables represent more complex underlying code and data.

## Encapsulation
The practice of keeping fields within a class private, then providing access to them via public methods. It's a protective barrier that keeps the data and code safe within the class itself.

## Inheritance
You let a new class adopt the properties of another. The inheriting class is usually called subclass or a child class, while the original one parent.

## Polymorphism
Use of the same word to mean different things in different contexts. Classes can be used with the same interface. A class that inherits attributes of another class can be called "polymorphic". Java supports two kinds of polymorphism:
- __Static polymorphism__ → you can overload a method with different sets of parameters. The compiler statically binds the method call to a specific method.
- __Dynamic polymorphism__ → a subclass can override a method of its superclass. If you instantiate the subclass, the JVM will always call the overridden method, even if you cast the subclass to its superclass.

---
## Composition
It describes a class that references one or more objects of other classes in instances variables. It allows you to reuse code without modeling an is-a association, as you do by using inheritance. In the real world, it's found quite regularly: a car has an engine but it's not one.

## Helper class
__Helper class__ → used to assist in providing some functionality, which isn't the main goal of the application or class in which it is used.
__Utility class__ → special case in which the methods are all static.

## Imperative vs. Declarative Programming
<center>“Imperative programming is like how you do something, and declarative programming is more like what you do”</center>

__Imperative programming__ → is concerned with how something is implemented, what are the necessary steps to accomplish something.\
__Declarative programming__ → is concerned with what you want to be done. You're describing what you're trying to achieve, without instructing how to do it. Many declarative approaches have some sort of underlying imperative abstraction.

# Sources
[Stackify](https://stackify.com)\
[Imperative vs Declarative Programming - U;](https://ui.dev/imperative-vs-declarative-programming/)\
[Helper class - Wikipedia](https://en.wikipedia.org/wiki/Helper_class)