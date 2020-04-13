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

<table class="alt">
<tbody><tr><th>Abstract class</th><th>Interface</th></tr>
<tr><td>1) Abstract class can <strong>have abstract and non-abstract</strong> methods.</td><td>Interface can have <strong>only abstract</strong> methods. Since Java 8, it can have <strong>default and static methods</strong> also.</td></tr>
<tr><td>2) Abstract class <strong>doesn't support multiple inheritance</strong>.</td><td>Interface <strong>supports multiple inheritance</strong>.</td></tr>
<tr><td>3) Abstract class <strong>can have final, non-final, static and non-static variables</strong>.</td><td>Interface has <strong>only static and final variables</strong>.</td></tr>
<tr><td>4) Abstract class <strong>can provide the implementation of interface</strong>.</td><td>Interface <strong>can't provide the implementation of abstract class</strong>.</td></tr>
<tr><td>5) The <strong>abstract keyword</strong> is used to declare abstract class.</td><td>The <strong>interface keyword</strong> is used to declare interface.</td></tr>
<tr><td>6) An <strong>abstract class</strong> can extend another Java class and implement multiple Java interfaces.</td><td>An <strong>interface</strong> can extend another Java interface only.</td></tr>
<tr><td>7) An <strong>abstract class</strong> can be extended using keyword "extends".</td><td> An <strong>interface</strong> can be implemented using keyword "implements".</td></tr>
<tr><td>8) A Java <strong>abstract class</strong> can have class members like private, protected, etc.</td><td>Members of a Java interface are public by default. </td></tr>
<tr><td>9)<strong>Example:</strong><br> public abstract class Shape{<br>public abstract void draw();<br>}</td><td><strong>Example:</strong><br> public interface Drawable{<br>void draw();<br>}</td></tr>
</tbody></table>
