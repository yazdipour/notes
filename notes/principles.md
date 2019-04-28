# _

Event Driven Programming
https://en.wikipedia.org/wiki/Event-driven_programming
https://www.techopedia.com/definition/7083/event-driven-program
https://dzone.com/articles/what-is-event-driven-programming-and-why-is-it-so

## Basics

* Boilerplate code means a piece of code which can be used over and over again. On the other hand, anyone can say that it's a piece of reusable code.

## UML

* Activity Diagram
* State Diagram
* Sequence Diagram
* Class Diagram

## OOP

* Inheritance:
* Encapsulation:
* Polymorphism:
* Abstraction:
* Inversion of Control: 2 dbClass with one interface - class using an obj type interface  - call class method with dbClass obj
* Dependency Injection

## Refactoring

---

## SOILID

* Single responsibility principle: a class should have only a single responsibility (i.e. only changes to one part of the software's specification should be able to affect the specification of the class). [Each class should have one single Goal, Do not merge Graphic methods with Navigation methods]
* Open/closed principle: "software entities … should be open for extension, but closed for modification." [Abstract classes with a specific goal and Do not have dependencies on other sections!]
* Liskov substitution principle: "objects in a program should be replaceable with instances of their subtypes without altering the correctness of that program." See also design by contract. [Ostrich can't be a subclass of BirdClass with Flying function]
* Interface segregation principle: "many client-specific interfaces are better than one general-purpose interface." [Use small Interfaces not Big one with lots of methods]
* Dependency inversion principle: one should "depend upon abstractions, [not] concretions." [1. High-level Modules should not depend on low-level modules, both should depend on abstractions. 2. Abstractions should not depend on details, must be vice-versa.] + [Using Interfaces to separate implementation and have a dependency on Interfaces/Abstractions, not implementations]

## IoC/DI

IoC is a generic term meaning rather than having the application call the methods in a framework, the framework calls implementations provided by the application.

DI is a form of IoC, where implementations are passed into an object through constructors/setters/service lookups, which the object will 'depend' on in order to behave correctly.

IoC without using DI, for example would be the Template pattern because the implementation can only be changed through sub-classing.

DI Frameworks are designed to make use of DI and can define interfaces (or Annotations in Java) to make it easy to pass in the implementations.

IoC Containers are DI frameworks that can work outside of the programming language. In some you can configure which implementations to use in metadata files (e.g. XML) which are less invasive.