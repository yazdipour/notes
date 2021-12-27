# _

Event Driven Programming
https://en.wikipedia.org/wiki/Event-driven_programming
https://www.techopedia.com/definition/7083/event-driven-program
https://dzone.com/articles/what-is-event-driven-programming-and-why-is-it-so

## Basics

* Boilerplate code means a piece of code which can be used over and over again. On the other hand, anyone can say that it's a piece of reusable code.

## UML

* https://sourcemaking.com/uml
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

* https://sourcemaking.com/refactoring

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

## DDD

[What I understand about domain-driven design](https://medium.com/code-thoughts/what-i-understand-about-domain-driven-design-f7fbd00e364f)

It feels like DDD is mostly about good object-oriented design presented in particular, formalized way with specific buzzwords (aggregate, bounded context, etc.).

DDD is also enforcing designing system around business domain, not around, e.g. database. That is usually a case when designing architecture from scratch quickly. As 99% of apps are CRUDs, ending up with database driven architectures would be natural. You usually start with file->new project, and go from there. This is not a problem for small apps, but might strike later when evolving the app. DDD solves that problem.

If you are familiar with [Clean Code](https://amzn.to/2BBzG84) and [SOLID](https://en.wikipedia.org/wiki/SOLID) design as presented in [Agile Principles, Patterns, and Practices in C#](https://amzn.to/2LxBMuv) then DDD does not bring much new concepts to the table. It may make you think more from a business perspective, and consider using new patterns ([Repository pattern](https://deviq.com/repository-pattern/), [CQRS](https://martinfowler.com/bliki/CQRS.html) or [Event Sourcing](https://martinfowler.com/eaaDev/EventSourcing.html)) though.

Going back to DDD terms (AKA buzzwords), they could be also summarized as follows:

- Ubiquitous Language – use meaningful names for classes, methods and variables
- Domain – be aware what problem you are solving
- Bounded Context – group objects that depends on each other
- Value Object – simple, immutable class
- Entity – class with unique identifier, usually used to represent persistent data
- Aggregate – group of related entities
- Repository – facade over your persistence layer to make it implementation agnostic
- Application Service – your system’s API
- Anti-corruption layer – layer for interaction with external system
- [CQRS (Command Query Responsibility Segregation)](https://martinfowler.com/bliki/CQRS.html) – separates querying for data and modifying data
- [Event Sourcing](https://martinfowler.com/eaaDev/EventSourcing.html) – storing changes to application state as a list of events, which allows to invoke and process events in producer/consumer fashion

Two main rules to Domain Driven Design:

- do not share models (and data)
  - It is better to repeat yourself than end up in complicated inheritance with switches.
  - It is not bad to have multiple customer classes in different contexts. Customer in search, in recommendations, in shopping card, in checkout, in shipping and in billing are different. In some cases those contexts do not overlap but when they do trouble starts.
- keep your business logic away from view and infrastructure
  - DDD people suggest having infrastructure and view layer but there are different ways to achieve this. Most important is to keep it away from especially persistence layer, as that is what often happening . This is hard to reach if you do not repeat yourself – see point above. When your model is complicated you have complicated ways to retrieve data and you end up coupling business logic with persistence layer. Simplest models can be easily stored even in files as JSON files.
