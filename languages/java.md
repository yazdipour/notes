# Java

## Genrice

```java
public <E> void printArray( E[] inputArray ) {}

public static <T extends Comparable<T>> T maximum(T x, T y, T z) {
      T max = x;   // assume x is initially the largest
      if(y.compareTo(max) > 0)
         max = y;   // y is the largest so far
      if(z.compareTo(max) > 0)
         max = z;   // z is the largest now
      return max;   // returns the largest object
}}

//CLASS
public class Box<T> {
   private T t;
```

## Lambda

```java
map.setOnMapLongClickListener(this::markOnHoldLocation);
map.setOnMapLongClickListener(latLng -> markOnHoldLocation(latLng));
```

## Abstract vs Interface

<table><tbody><tr><th>Abstract class</th><th>Interface</th></tr><tr><td>1) Abstract class can have abstract and non-abstract methods.</td><td>Interface can have only abstract methods. Since Java 8, it can have default and static methods also.</td></tr><tr><td>2) Abstract class doesn't support multiple inheritance.</td><td>Interface supports multiple inheritance.</td></tr><tr><td>3) Abstract class can have final, non-final, static and non-static variables.</td><td>Interface has only static and final variables.</td></tr><tr><td>4) Abstract class can provide the implementation of interface.</td><td>Interface can't provide the implementation of abstract class.</td></tr><tr><td>5) The abstract keyword is used to declare abstract class.</td><td>The interface keyword is used to declare interface.</td></tr><tr><td>6) An abstract class can extend another Java class and implement multiple Java interfaces.</td><td>An interface can extend another Java interface only.</td></tr><tr><td>7) An abstract class can be extended using keyword "extends".</td><td>An interface can be implemented using keyword "implements".</td></tr><tr><td>8) A Java abstract class can have class members like private, protected, etc.</td><td>Members of a Java interface are public by default.</td></tr><tr><td>9)Example: `public abstract class Shape{  public abstract void draw();}` </td><td>Example:  `public interface Drawable{  void draw();}` </td></tr></tbody></table>
