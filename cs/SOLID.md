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

# Sources
[Stackify](https://stackify.com/)\
[SOLID Principles every Developer Should Know – Bits and Pieces](https://blog.bitsrc.io/solid-principles-every-developer-should-know-b3bfa96bb688)\
[S.O.L.I.D The first 5 principles of Object Oriented Design with JavaScript – Medium](https://medium.com/@cramirez92/s-o-l-i-d-the-first-5-priciples-of-object-oriented-design-with-javascript-790f6ac9b9fa)
