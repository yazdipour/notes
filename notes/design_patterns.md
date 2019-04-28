# Design Patterns

MVP
https://antonioleiva.com/mvp-android/
https://medium.com/cr8resume/make-you-hand-dirty-with-mvp-model-view-presenter-eab5b5c16e42
https://android.jlelse.eu/why-to-choose-mvvm-over-mvp-android-architecture-33c0f2de5516
https://medium.com/upday-devs/android-architecture-patterns-part-3-model-view-viewmodel-e7eeee76b73b
https://github.com/googlesamples/android-architecture
https://github.com/googlesamples/android-architecture/tree/todo-mvp-rxjava/

## Sample

* Lynda Course: In Java https://github.com/derekwzheng/design-patterns
* https://github.com/iluwatar/java-design-patterns/

## Creational Patterns
https://sourcemaking.com/design_patterns/structural_patterns

### Object Pool / Resource Pool
* Object pooling can offer a significant performance boost; it is most effective in situations where the cost of initializing a class instance is high, the rate of instantiation of a class is high, and the number of instantiations in use at any one time is low.
* Sample: https://sourcemaking.com/design_patterns/object_pool/java

### Prototype
Specify the kinds of objects to create using a prototypical instance, and create new objects by copying this prototype.
Sample: https://sourcemaking.com/design_patterns/prototype/java/1

### Abstract Factory
* Provide an interface for creating families of related or dependent objects without specifying their concrete classes.
* A hierarchy that encapsulates: many possible “platforms”, and the construction of a suite of “products”.
* The new operator considered harmful.
* Sample: https://sourcemaking.com/design_patterns/abstract_factory/java/2

### Factory Method

* Define an interface for creating an object, but let subclasses decide which class to instantiate. Factory Method lets a class defer instantiation to subclasses.
* Sample: https://sourcemaking.com/design_patterns/factory_method/java/1

```java
public class PizzaFactory1 extends IPizzaFactory{
    public Pizza createPizza(String type) {
        Pizza pizza = null;
        if (type.equals("cheese")) pizza = new CheesePizza();
        else if (type.equals("pepperoni")) pizza = new PepperoniPizza();
        return pizza;
    }
public class PizzaFactory2 extends IPizzaFactory{
    public Pizza createPizza(String type) {
        ...
//
public class PizzaStore {
    IPizzaFactory factory;
    public PizzaStore(IPizzaFactory factory) {
        this.factory = factory;
    }
    public Pizza orderPizza(String type) {
        Pizza pizza = factory.createPizza(type);
        pizza.bake();
        pizza.cut();
        pizza.box();
        return pizza;
    }
```

### Singleton

Only a single instance can exist

```c#
public static class ApiHandler
{   //Semi Singleton Sample!
    private static IApi api;
    public static IApi Api => api ?? (api = Refit.RestService.For<IApi>("http://x.com"));
}
```

Thread Safe Singleton in JAVA

```java
public class Singleton {
    private static Singleton uniqueInstance;
    public static **synchronized** Singleton getInstance() {...
```

## Structural Patterns

### Builder
* Separate the construction of a complex object from its representation so that the same construction process can create different representations.
* Parse a complex representation, create one of several targets.
* Sample: https://sourcemaking.com/design_patterns/builder/java/2

### Adapter
Match interfaces of different classes

### Bridge
Separates an object’s interface from its implementation

### Composite
A tree structure of simple and composite objects

### Facade
A single class that represents an entire subsystem

### Flyweight
A fine-grained instance used for efficient sharing

### Proxy
An object representing another object

### Decorator

Add responsibilities to objects dynamically. It create new object from the previous one with another layer (decorator) on it.

```java
public static void main(String args[]) {
    Beverage beverage2 = new Espresso();
    beverage2 = new Milk(beverage2);
    beverage2 = new Mocha(beverage2);
    System.out.println(beverage2.getDescription() + " $" + beverage2.cost());
    // Espresso Cofffe, Milk, Mocha $ 2.0
}
//
public abstract class Beverage {
    String description = "Unknown Beverage";
    public String getDescription() { return description; }
    public abstract double cost();
}
public class Espresso extends Beverage {
public class Decaf extends Beverage {
    public Decaf() { description = "Decaf Coffee";    }
    public double cost() { return 1.05; }
}
//
public abstract class CondimentDecorator extends Beverage {
    public abstract String getDescription();
}
public class Milk extends CondimentDecorator {
public class Mocha extends CondimentDecorator {
    Beverage beverage;
    public Mocha(Beverage beverage) {
        this.beverage = beverage;
    }
    public String getDescription() {
        return beverage.getDescription() + ", Mocha";
    }
    public double cost() {
        return .20 + beverage.cost();
    }
}
```

## Behavioral Patterns
https://sourcemaking.com/design_patterns/behavioral_patterns

### Chain of Responsibility
A way of passing a request between a chain of objects

### Command
Encapsulate a command request as an object

### Interpreter
A way to include language elements in a program

### Mediator
Defines simplified communication between classes

### Memento
Capture and restore an object’s internal state

### Template
Defer the exact steps of an algorithm to a subclass

### Visitor
Defines a new operation to a class without change

#### Null Object
Designed to act as a default value of an object

### Iterator/Collection

Kinda like `inteface for array, arraylist, vector, linkedlist`. With `hasNext, next, remove,...` mothods.

```java
public interface Menu {
    public Iterator<String> createIterator();
}

public class PancakeHouseMenu implements Menu {
    ArrayList<String> menuItems;
    public Iterator<String> createIterator() {
        return menuItems.iterator();
```

There is a built-in Iterator for arraylist, vector, linkedlist. But for Array you have to impl remove() by yourself.

```java
public class DinerMenuIterator implements Iterator<String> {
    String[] list;
    int position = 0;

    public DinerMenuIterator(String[] list) { this.list = list; }

    public String next() { return list[position++]; }

    public boolean hasNext() { return !(position >= list.length || list[position] == null);}
  
    public void remove() {
        if (position <= 0)
            throw new IllegalStateException
                ("You can't remove an item until you've done at least one next()");
        if (list[position-1] != null) {
            for (int i = position-1; i < (list.length-1); i++)
                list[i] = list[i+1];
            list[list.length-1] = null;
        }
    }
}
```

### State

Alter an object’s behavior when its state changes / Instead of using enum and ints to change State and behavior, impl different behavior State in their classes which is inherited by IState.

```java
public class GumballMachine {
    State soldOutState;
    State noQuarterState;
    State hasQuarterState;
    State soldState;
    State state = soldOutState;
    public GumballMachine(int numberGumballs) {
        soldOutState = new SoldOutState(this);
        noQuarterState = new NoQuarterState(this);
        hasQuarterState = new HasQuarterState(this);
        soldState = new SoldState(this);
    }
    void refill(int count) {
        state = noQuarterState;
    }
//
public interface State {
    public void insertQuarter();
    public void ejectQuarter();
    public void turnCrank();
    public void dispense();
}
public class SoldState implements State {
    GumballMachine gumballMachine;
    public SoldState(GumballMachine gumballMachine) {
        this.gumballMachine = gumballMachine;
```

### Observer

* A way of notifying change to a number of classes. Publisher will send changes to Subscribers, like News Mail Services.
* It is loosely coupled
* Can Impl by yourself, but there are lots of prewritten libraries we can use.
* Observable = Publisher = Subject
    * `registerObserver()`
    * `removeObserver()`
    * `notifyObserver()`
    * `setChanged()`
* Observer = Subscriber = Dependent
    * `update()`

Sample WeatherData Publisher

```java
public static void main(String[] args) {
    // Observable
    WeatherData weatherData = new WeatherData();
    // Observer + registering
    StatisticsDisplay statisticsDisplay = new StatisticsDispla(weatherData);
    // Observer2
    ForecastDisplay forecastDisplay = new ForecastDispla(weatherData);
    //Change Data
    weatherData.setMeasurements(72);
}
// Observable / Publisher
import java.util.Observable;
import java.util.Observer;
public class WeatherData extends Observable {
    private float temperature;
    public void setMeasurements(float temperature) {
        this.temperature = temperature;
        setChanged();
        notifyObservers();
    }
// Observer
public class StatisticsDisplay implements Observer {
    public StatisticsDisplay(Observable observable) {
        observable.addObserver(this);
    }
    public void update(Observable observable, Object arg) {
        // Use if: cause u can observe multiple observables
        if (observable instanceof WeatherData) {
            WeatherData weatherData = (WeatherData)observable;
            // do stuff
```

### Strategy (x Has y Behavior)

* In Parent Class, put behaviors with Interfaces so you cloud be able to modify behaviors in Child class.
* Ex. in IDuck, we have IFlyBehavior object, so that in the RubberDuck class, you set its custom behavior like, FlyBehaviorRubber.
* It's all about using Interfaces when you want to change implementations.

```java
public abstract class Duck {
    IFlyBehavior flyBehavior;
    QuackBehavior quackBehavior;
    public void setFlyBehavior(IFlyBehavior fb) { flyBehavior = fb; }
    public void performFly() { flyBehavior.fly(); }
}
public class DecoyDuck extends Duck {
    public DecoyDuck() {
        setFlyBehavior(new FlyNoWay());
    }
//FlyBehavior
public interface FlyBehavior {
	public void fly();
}
public class FlyNoWay implements FlyBehavior {...
public class FlyWithWings implements FlyBehavior {...
```

## Compound Patterns

### MVVM

### MVP

### MVC

* Combines Strategy, Observer and Composite patterns
* Used to separate there parts: User interface, Logic, DataModel

```c
#http://x.com/users/profile/1

/routes
    users/profile/:id = Users.getProfile(id)
/controllers
    class Users{
        function getProfile(id){
            profile = this.UserModel.getProfile(id)
            renderView('users/profile', profile)

/models
    class UserModel{
        function getProfile(id){
            return this.db.get('SELECT * FROM users WHERE id='+id);

/views
    /users
        /profile
            <h1>{{profile.name}}</h1>
```

## Antipatterns