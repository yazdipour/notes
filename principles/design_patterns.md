# Design Patterns

## Samples

* Lynda Course in Java https://github.com/derekwzheng/design-patterns
* https://github.com/iluwatar/java-design-patterns/
* https://sourcemaking.com/design_patterns/ 

## Creational Patterns

all about class instantiation

### Object Pool / Resource Pool

* Significant performance boost
* it is most effective in situations where the cost of initializing a class instance is high, the rate of instantiation of a class is high, and the number of instantiations in use at any one time is low.
* How? Have to have `public abstract class ObjectPool<T>` with some abstract methods of managing pool of objects. Then Classes need to extends `ObjectPool<X>` to impl reusability and ... logics base on the usage.
* More Details: https://sourcemaking.com/design_patterns/object_pool
* Sample: https://sourcemaking.com/design_patterns/object_pool/java

### Prototype

Specify the kinds of objects to create using a prototypical instance, and create new objects by copying this prototype.

* More Details: https://sourcemaking.com/design_patterns/prototype
* Sample2: https://sourcemaking.com/design_patterns/prototype/java/2

```java
//PrototypeFactory
public class PrototypeFactory {
    public static void main(String[] args) {
        for (String type : args) {
            Person prototype = Factory.getPrototype(type);
            System.out.println(prototype);
// Factory
class Factory {
    private static final Map<String, Person> prototypes = new HashMap<>();
    static {
        prototypes.put("tom", new Tom());
        prototypes.put("dick", new Dick());
    }
    public static Person getPrototype(String type) {
        try {
            return prototypes.get(type).clone();
        } catch (NullPointerException ex) {
            System.out.println(type + ", doesn't exist");
// Types
interface Person {
    Person clone();
}
class Dick implements Person {
class Tom implements Person {
private final String NAME = "Tom";
    @Override
    public Person clone() { return new Tom(); }
}

```

### Factory Method (Abstract Factory Similar)

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

### Builder

* Instead of Passing all obj property by Constructor, 
* Separate the construction of a complex object from its representation so that the same construction process can create different representations.

```c#
// Usage
var api = new ApiHandler()
            .setBaseUrl("x.com");
// Builder
class ApiHandler
{
    private String base_url;
    public ApiHandler setBaseUrl(String base_url)
    {
        this.base_url = base_url;
    }
```

## Structural Patterns

define ways to compose objects to obtain new functionality.

### Adapter

* We have Line,Rectangle Classes with no parent and with same `Draw()` method. Now we create `IShape` interface with `DrawAdapter & LineAdapter` implementing `IShape`.

```java
class Line {
    public void draw(int x1, int y1, int x2, int y2) {
class Rectangle {
    public void draw(int x, int y, int width, int height) {
//Adapter
interface Shape {
    void draw(int x1, int y1, int x2, int y2);
class LineAdapter implements Shape {
    @Override
        public void draw(int x1, int y1, int x2, int y2) {
            adaptee.draw(x1, y1, x2, y2);
class RectangleAdapter implements Shape {
    @Override
    public void draw(int x1, int y1, int x2, int y2) {
        int x = Math.min(x1, x2);
        int y = Math.min(y1, y2);
        int width = Math.abs(x2 - x1);
        int height = Math.abs(y2 - y1);
        adaptee.draw(x, y, width, height);
// Usage
Shape l = new LineAdapter(), r = new RectangleAdapter();
l.draw(...); r.draw(...);
```

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

### Bridge (Handle-Body Pattern)

* Separates interface from its implementation.
* Ex. We have `Switch` interface, but in each Class we have different impl of `Switch`.
![Bridge](https://sourcemaking.com/files/v2/content/patterns/Bridge_example.png)

### Composite

* A tree structure of simple and composite objects
* 1-to-many "has a" up the "is a" hierarchy

### Facade

* A single class that represents an entire subsystem
* Wrap a complicated subsystem with a simpler interface.

### Flyweight

* Use sharing to support large numbers of fine-grained objects efficiently.

### Proxy

* Just a wrapper for other libraries!
* X_LIBRARY <---> PROXY <---> MyApp
* Provide a surrogate or placeholder for another object to control access to it.
* Sample https://sourcemaking.com/design_patterns/proxy/java/1

## Behavioral Patterns

* most specifically concerned with communication between objects.
* https://sourcemaking.com/design_patterns/behavioral_patterns

### Chain of Responsibility

A way of passing a request between a chain of objects

### Command

Encapsulate a command request as an object

### Interpreter

A way to include language elements in a program

### Mediator

Defines simplified communication between classes

### Memento

* Capture and restore an object’s internal state
* Promote undo or rollback to full object status.
* A magic cookie that encapsulates a "check point" capability.
* https://sourcemaking.com/design_patterns/memento/

### Template

* Defer the exact steps of an algorithm to a subclass

### Visitor

Defines a new operation to a class without change

### Null Object

Designed to act as a default value of an object

### Iterator/Collection

Kinda like inteface for `array, arraylist, vector, linkedlist`. With `hasNext, next, remove,...` mothods.

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

## Architecture / Compound Patterns

[Visit Architecture Page](https://yazdipour.github.io/notes/#/principles/architecture.md)