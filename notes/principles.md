# _

Event Driven Programming
https://en.wikipedia.org/wiki/Event-driven_programming
https://www.techopedia.com/definition/7083/event-driven-program
https://dzone.com/articles/what-is-event-driven-programming-and-why-is-it-so

MVP
https://antonioleiva.com/mvp-android/
https://medium.com/cr8resume/make-you-hand-dirty-with-mvp-model-view-presenter-eab5b5c16e42
https://android.jlelse.eu/why-to-choose-mvvm-over-mvp-android-architecture-33c0f2de5516
https://medium.com/upday-devs/android-architecture-patterns-part-3-model-view-viewmodel-e7eeee76b73b
https://github.com/googlesamples/android-architecture
https://github.com/googlesamples/android-architecture/tree/todo-mvp-rxjava/

MVC
MVVM
State Machines
SOAP

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

* Dependency Injection:

## Design Patterns

* Singleton: A class of which only a single instance can exist

* Builder
* Factory
* Bridge
* Decorator
* Facade
* Proxy
* Mediator
* Observable
* Adapter
* MVVM
* MVC
* MVP

## Antipatterns

## Refactoring

## SOILID

* Single responsibility principle: a class should have only a single responsibility (i.e. only changes to one part of the software's specification should be able to affect the specification of the class). [Each class should have one single Goal, Do not merge Graphic methods with Navigation methods]
* Open/closed principle: "software entities … should be open for extension, but closed for modification." [Abstract classes with a specific goal and Do not have dependencies on other sections!]
* Liskov substitution principle: "objects in a program should be replaceable with instances of their subtypes without altering the correctness of that program." See also design by contract. [Ostrich can't be a subclass of BirdClass with Flying function]
* Interface segregation principle: "many client-specific interfaces are better than one general-purpose interface." [Use small Interfaces not Big one with lots of methods]
* Dependency inversion principle: one should "depend upon abstractions, [not] concretions." [1. High-level Modules should not depend on low-level modules, both should depend on abstractions. 2. Abstractions should not depend on details, must be vice-versa.] + [Using Interfaces to separate implementation and have a dependency on Interfaces/Abstractions, not implementations]