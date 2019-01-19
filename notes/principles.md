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

### MVVM
### MVC
### MVP

### Creational patterns
https://sourcemaking.com/design_patterns/creational_patterns

#### Singleton

A class of which only a single instance can exist

```c#
    public static class ApiHandler
    {   //Semi Singleton Sample!
        private static IApi api;
        public static IApi Api => api ?? (api = Refit.RestService.For<IApi>("http://x.com"));
    }
```

#### Prototype

Specify the kinds of objects to create using a prototypical instance, and create new objects by copying this prototype.

Sample: https://sourcemaking.com/design_patterns/prototype/java/1

#### Object Pool / Resource Pool

* Object pooling can offer a significant performance boost; it is most effective in situations where the cost of initializing a class instance is high, the rate of instantiation of a class is high, and the number of instantiations in use at any one time is low.
* Sample: https://sourcemaking.com/design_patterns/object_pool/java

#### Builder

* Separate the construction of a complex object from its representation so that the same construction process can create different representations.
* Parse a complex representation, create one of several targets.
* Sample: https://sourcemaking.com/design_patterns/builder/java/2

#### Factory Method

* Define an interface for creating an object, but let subclasses decide which class to instantiate. Factory Method lets a class defer instantiation to subclasses.
* Defining a “virtual” constructor.
* The new operator considered harmful.
* Sample: https://sourcemaking.com/design_patterns/factory_method/java/1

#### Abstract Factory

* Provide an interface for creating families of related or dependent objects without specifying their concrete classes.
* A hierarchy that encapsulates: many possible “platforms”, and the construction of a suite of “products”.
* The new operator considered harmful.
* Sample: https://sourcemaking.com/design_patterns/abstract_factory/java/2

### Structural patterns
https://sourcemaking.com/design_patterns/structural_patterns

#### Adapter
Match interfaces of different classes
#### Bridge
Separates an object’s interface from its implementation
#### Composite
A tree structure of simple and composite objects
#### Decorator
Add responsibilities to objects dynamically
#### Facade
A single class that represents an entire subsystem
#### Flyweight
A fine-grained instance used for efficient sharing
#### Private Class Data
Restricts accessor/mutator access
#### Proxy
An object representing another object

### Behavioral patterns
https://sourcemaking.com/design_patterns/behavioral_patterns
#### Chain of responsibility
A way of passing a request between a chain of objects
#### Command
Encapsulate a command request as an object
#### Interpreter
A way to include language elements in a program
#### Iterator
Sequentially access the elements of a collection
#### Mediator
Defines simplified communication between classes
#### Memento
Capture and restore an object’s internal state
#### Null Object
Designed to act as a default value of an object
#### Observer
A way of notifying change to a number of classes
#### State
Alter an object’s behavior when its state changes
#### Strategy
Encapsulates an algorithm inside a class
#### Template method
Defer the exact steps of an algorithm to a subclass
#### Visitor
Defines a new operation to a class without change

## Antipatterns

???

## Refactoring

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