# String Format Cheatsheet

```java
//INDEX
String.format("%2$s", 32, "Hello"); // prints: "Hello"
//Numbers
String.format("|%20d|", 93); // prints: |                  93|
String.format("|%-20d|", 93); // prints: |93                  |
String.format("|%020d|", 93); // prints: |00000000000000000093|
String.format("|%+20d|", 93); // prints: |                 +93|
String.format("|%,d|", 10000000); // prints: |10,000,000|
String.format("|%(d|", -36); // prints: |(36)|
//Octal 
String.format("|%o|"), 93); // prints: 135
//Hex
String.format("|%x|", 93); // prints: 5d
String.format("|%#x|", 93);// prints: 0x5d
String.format("|%#X|", 93);// prints: 0X5D
//Stirngs
String.format("|%s|", "Hello World"); // prints: "Hello World"
String.format("|%30s|", "Hello World"); // prints: | Hello World|
String.format("|%.5s|", "Hello World"); // |Hello| => Specify Maximum Number of Chars
String.format("|%30.5s|", "Hello World"); //| Hello| =>Field Width and Maximum Number of Chars

```

## Format Specifiers

<table> 
 <thead> 
  <tr> 
   <td>Specifier</td> 
   <td>Applies to</td> 
   <td>Output</td> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td>%a</td> 
   <td>floating point (except&nbsp;<a href="https://docs.oracle.com/javase/8/docs/api/java/math/BigDecimal.html" rel="nofollow"><em>BigDecimal</em></a>)</td> 
   <td>Hex output of floating point number</td> 
  </tr> 
  <tr> 
   <td>%b</td> 
   <td>Any type</td> 
   <td>“true” if non-null, “false” if null</td> 
  </tr> 
  <tr> 
   <td>%c</td> 
   <td>character</td> 
   <td>Unicode character</td> 
  </tr> 
  <tr> 
   <td>%d</td> 
   <td>integer (incl. byte, short, int, long, bigint)</td> 
   <td>Decimal Integer</td> 
  </tr> 
  <tr> 
   <td>%e</td> 
   <td>floating point</td> 
   <td>decimal number in scientific notation</td> 
  </tr> 
  <tr> 
   <td>%f</td> 
   <td>floating point</td> 
   <td>decimal number</td> 
  </tr> 
  <tr> 
   <td>%g</td> 
   <td>floating point</td> 
   <td>decimal number, possibly in scientific notation depending on the precision and value.</td> 
  </tr> 
  <tr> 
   <td>%h</td> 
   <td>any type</td> 
   <td>Hex String of value from hashCode() method.</td> 
  </tr> 
  <tr> 
   <td>&nbsp;%n</td> 
   <td>none</td> 
   <td>Platform-specific line separator.</td> 
  </tr> 
  <tr> 
   <td>%o</td> 
   <td>integer (incl. byte, short, int, long, bigint)</td> 
   <td>Octal number</td> 
  </tr> 
  <tr> 
   <td>%s</td> 
   <td>any type</td> 
   <td>String value</td> 
  </tr> 
  <tr> 
   <td>%t</td> 
   <td>Date/Time (incl. long, Calendar, Date and TemporalAccessor)</td> 
   <td>%t is the prefix for Date/Time conversions. More formatting flags are needed after this. See Date/Time conversion below.</td> 
  </tr> 
  <tr> 
   <td>%x</td> 
   <td>integer (incl. byte, short, int, long, bigint)</td> 
   <td><p>Hex string.</p></td> 
  </tr> 
 </tbody> 
</table> 

## Date and Time Formatting

<table> 
 <thead> 
  <tr> 
   <td width="15%">&nbsp;Flag</td> 
   <td>Notes</td> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td>&nbsp;%tA</td> 
   <td>Full name of the day of the week, e.g. “<code>Sunday</code>“, “<code>Monday</code>“</td> 
  </tr> 
  <tr> 
   <td>&nbsp;%ta</td> 
   <td>Abbreviated name of the week day e.g. “<code>Sun</code>“, “<code>Mon</code>“, etc.</td> 
  </tr> 
  <tr> 
   <td>&nbsp;%tB</td> 
   <td>Full name of the month e.g. “<code>January</code>“, “<code>February</code>“, etc.</td> 
  </tr> 
  <tr> 
   <td>&nbsp;%tb</td> 
   <td>Abbreviated month name e.g. “<code>Jan</code>“, “<code>Feb</code>“, etc.</td> 
  </tr> 
  <tr> 
   <td>&nbsp;%tC</td> 
   <td>Century part of year formatted with two digits e.g. “00” through “99”.</td> 
  </tr> 
  <tr> 
   <td>&nbsp;%tc</td> 
   <td>Date and time formatted with “<code>%ta %tb %td %tT %tZ %tY</code>” e.g. “<code>Fri Feb 17 07:45:42 PST 2017</code>“</td> 
  </tr> 
  <tr> 
   <td>&nbsp;%tD</td> 
   <td>Date formatted as “<code>%tm/%td/%ty</code>“</td> 
  </tr> 
  <tr> 
   <td>&nbsp;%td</td> 
   <td>Day of the month formatted with two digits. e.g. “<code>01</code>” to “<code>31</code>“.</td> 
  </tr> 
  <tr> 
   <td>&nbsp;%te</td> 
   <td>Day of the month formatted without a leading 0 e.g. “1” to “31”.</td> 
  </tr> 
  <tr> 
   <td>%tF</td> 
   <td>ISO 8601 formatted date with “<code>%tY-%tm-%td</code>“.</td> 
  </tr> 
  <tr> 
   <td>%tH</td> 
   <td>Hour of the day for the 24-hour clock e.g. “<code>00</code>” to “<code>23</code>“.</td> 
  </tr> 
  <tr> 
   <td>%th</td> 
   <td>Same as %tb.</td> 
  </tr> 
  <tr> 
   <td>%tI</td> 
   <td>Hour of the day for the 12-hour clock e.g. “<code>01</code>” – “<code>12</code>“.</td> 
  </tr> 
  <tr> 
   <td>%tj</td> 
   <td>Day of the year formatted with leading 0s e.g. “<code>001</code>” to “<code>366</code>“.</td> 
  </tr> 
  <tr> 
   <td>%tk</td> 
   <td>Hour of the day for the 24 hour clock without a leading 0 e.g. “<code>0</code>” to “<code>23</code>“.</td> 
  </tr> 
  <tr> 
   <td>%tl</td> 
   <td>Hour of the day for the 12-hour click without a leading 0 e.g. “<code>1</code>” to “<code>12</code>“.</td> 
  </tr> 
  <tr> 
   <td>%tM</td> 
   <td>Minute within the hour formatted a leading 0 e.g. “<code>00</code>” to “<code>59</code>“.</td> 
  </tr> 
  <tr> 
   <td>%tm</td> 
   <td>Month formatted with a leading 0 e.g. “<code>01</code>” to “<code>12</code>“.</td> 
  </tr> 
  <tr> 
   <td>%tN</td> 
   <td>Nanosecond formatted with 9 digits and leading 0s e.g. “000000000” to “999999999”.</td> 
  </tr> 
  <tr> 
   <td>%tp</td> 
   <td>Locale specific “am” or “pm” marker.</td> 
  </tr> 
  <tr> 
   <td>%tQ</td> 
   <td>Milliseconds since epoch Jan 1 , 1970 00:00:00 UTC.</td> 
  </tr> 
  <tr> 
   <td>%tR</td> 
   <td>Time formatted as 24-hours e.g. “<code>%tH:%tM</code>“.</td> 
  </tr> 
  <tr> 
   <td>%tr</td> 
   <td>Time formatted as 12-hours e.g. “<code>%tI:%tM:%tS %Tp</code>“.</td> 
  </tr> 
  <tr> 
   <td>%tS</td> 
   <td>Seconds within the minute formatted with 2 digits e.g. “00” to “60”. “60” is required to support leap seconds.</td> 
  </tr> 
  <tr> 
   <td>%ts</td> 
   <td>Seconds since the epoch Jan 1, 1970 00:00:00 UTC.</td> 
  </tr> 
  <tr> 
   <td>%tT</td> 
   <td>Time formatted as 24-hours e.g. “<code>%tH:%tM:%tS</code>“.</td> 
  </tr> 
  <tr> 
   <td>%tY</td> 
   <td>Year formatted with 4 digits e.g. “<code>0000</code>” to “<code>9999</code>“.</td> 
  </tr> 
  <tr> 
   <td>%ty</td> 
   <td>Year formatted with 2 digits e.g. “<code>00</code>” to “<code>99</code>“.</td> 
  </tr> 
  <tr> 
   <td>%tZ</td> 
   <td>Time zone abbreviation. e.g. “<code>UTC</code>“, “<code>PST</code>“, etc.</td> 
  </tr> 
  <tr> 
   <td>%tz</td> 
   <td><p>Time Zone Offset from GMT e.g. “</p><code>-0800</code><p>“.</p></td> 
  </tr> 
 </tbody> 
</table> 