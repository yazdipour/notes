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