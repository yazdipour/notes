# Java

## Basic Spring Controller Test

```java
@RunWith(SpringRunner.class)
@WebMvcTest(LoggingController.class)
class LoggingControllerTest {

    @Autowired
    private MockMvc mvc;

    @Test
    void testLog() throws Exception {
        mvc.perform(MockMvcRequestBuilders.post("/"))
                .andExpect(content().string("Check out the Logs to see the output..."));

      //   mvc.perform(get(VERSION + USERS + "all")
      //           .with(user("blaze").password("Q1w2e3r4"))
      //           .contentType(APPLICATION_JSON))
      //           .andExpect(status().isOk())
      //           .andExpect(jsonPath("$", hasSize(1)))
      //           .andExpect(jsonPath("$[0].address", is(user.getAddress())));
    }
}
```

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

| JDK                                                                      | JRE                                                                         | JVM                                                                                                                           |
| ------------------------------------------------------------------------ | --------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| It stands for Java Development Kit.                                      | It stands for Java Runtime Environment.                                     | It stands for Java Virtual Machine.                                                                                           |
| It is the tool necessary to compile, document and package Java programs. | JRE refers to a runtime environment in which Java bytecode can be executed. | It is an abstract machine. It is a specification that provides a run-time environment in which Java bytecode can be executed. |
| It contains JRE + development tools.                                     | It’s an implementation of the JVM which physically exists.                  | JVM follows three notations: Specification, **Implementation,** and **Runtime Instance**.                                     |

| `this()`                                                  | `super()`                                                         |
| --------------------------------------------------------- | ----------------------------------------------------------------- |
| 1. this() represents the current instance of a class      | 1. super() represents the current instance of a parent/base class |
| 2. Used to call the default constructor of the same class | 2. Used to call the default constructor of the parent/base class  |
| 3. Used to access methods of the current class            | 3. Used to access methods of the base class                       |
| 4. Used for pointing the current class instance           | 4. Used for pointing the superclass instance                      |
| 5. Must be the first line of a block                      | 5. Must be the first line of a block                              |

Q8. What is method overloading and method overriding?
Method Overloading :

In Method Overloading, Methods of the same class shares the same name but each method must have a different number of parameters or parameters having different types and order.
Method Overloading is to “add” or “extend” more to the method’s behavior.

It is a compile-time polymorphism.
The methods must have a different signature.

It may or may not need inheritance in Method Overloading.

## Collection class

![collection](https://www.edureka.co/blog/wp-content/uploads/2017/05/Collection-framework-hierarchy.png)

## Job Interview Questions

1. تفاوت بین متدهای استاتیک و غیراستاتیک را توضیح دهید و همچنین نوع معماری حافظه که برای آن‌ها در نظر گرفته می‌شود را شرح دهید.

2. دلیل استفاده از کلیدواژۀ final را در کلاس‌ها و متغیرها توضیح دهید و موقعیت‌هایی را بیان کنید که می‌بایست از این کلیدواژه استفاده نمایید.

3. مفهوم Casting را در زبان جاوا توضیح دهید. فرض کنید یک داده از نوع عدد اعشاری (double) داریم؛ حال چگونه می‌توانیم این داده را در قالب دیتاتایپی از جنس عدد صحیح (int) نشان دهیم؟

4. مزایای اصلی استفاده از Polymorphism (چندریختی) چیست و چه جایگزینی می‌توان برای آن یافت؟

5. کانستراکتور را به کمک مفهوم وراثت در زبان جاوا توضیح دهید.

6. مفهوم Constructor Chaining در جاوا چیست؟

7. کلیدواژۀ super برای دسترسی به ویژگی‌های سوپرکلاس استفاده می‌شود اما هنگامی که شما مجاز به استفاده از آن نیستید، چگونه می‌توانید به ویژگی‌های سوپرکلاس دسترسی پیدا کنید؟

8. فرض کنید کتاب‌های کلاس یازدهم و دوازدهم خود را در اختیار دارید. حال چگونه از مفهوم ارث‌بری برای نشان دادن رابطۀ بین آن‌ها استفاده می‌کنید؟

9. چرا کامپایلر جاوا فقط به یک متد اصلی از جنس استاتیک نیاز دارد؟

10. کاربرد آرایه یا آبجکت به اصطلاح Anonymous (بی‌نام) در جاوا چیست؟

11. چه زمانی از کلاس‌های استاتیک یا غیراستاتیک استفاده می‌کنید؟

12. منظور از اصطلاح Abstraction در واقع پنهان‌ کردن اطلاعات است. حال این مفهوم چگونه در زبان جاوا شکل می‌گیرد و همچنین برنامه‌ای بنویسید که در آن Abstraction (انتزاع) را نشان دهید سپس این برنامه را بدون استفاده از انتزاع نیز بازنویسی کنید.

13. انواع روش‌های ایجاد یک آبجکت را توضیح دهید و بگویید که در حین ایجاد آبجکت چه زمانی به آن حافظه اختصاص خواهد یافت.

14. مراحل یک برنامه، از نوشتن کد تا اجرای آن بر روی سیستم، را توضیح دهید.

15. مفهوم تخصیص حافظۀ هیپ در جاوا را توضیح دهید. همچنین تفاوت میان حافظۀ اِستک و هیپ را شرح دهید.

16. توضیح دهید چگونه JVM برنامۀ شما را تفسیر می‌کند به علاوه اینکه چرخۀ اجرای کد را در زبان جاوا شرح دهید.

17. تفاوت بین کلدواژه‌های private ،public و protected را بیان کنید.

18. اگر در یک برنامهٔ جاوا متد اصلی private شود، چه نتیجه‌ای خواهد داشت؟

19. چگونه می‌توان به یک برنامۀ جاوا دستور داد تا عملیات خواندن فایل را با استفاده از آرگومانی در کامندلاین اجرا کند؟

20. در چه مواقعی به سوپر کانستراکتور نیاز دارید؟

21. در زبان جاوا یک برنامه را می‌توان هم از طریق اینترفیس و هم اَبستِرکت کلاس نوشت؛ بنابراین چرا نیاز به اینترفیس داریم؟

22. وراثت چندسطحی (Multilevel Inheritance) در جاوا چیست و آیا جاوا ارث‌بری چندگانه (Multiple) را پشتیبانی می‌کند؟

23. جاوا زبانی شییٔ‌گرا (OOP) است. این اصطلاح را توضیح دهید.

24. مفهوم الگوهای طراحی (Design Patterns) را در جاوا را توضیح دهید. اگر ملزم به طراحی الگوهای اختصاصی خود باشید، به چه پارامترهایی بیشتر توجه خواهید کرد؟

25. برنامه‌های زیر را بنویسید:

- برنامه‌ای بنویسید که یک رشته یا عدد را از کاربر دریافت کرده و اگر از هر دو سمت به طور یکسان خوانده می‌شد، به کاربر نشان دهد.
- یک رشته از کاربر دریافت کرده و در خروجی معکوس آن را نشان دهید.
- آرایه‌ای از اعداد را از کاربر دریافت کرده، مینیمم و ماکسیمم آن را بیابید.
- فرض کنید یک آرایۀ خالی با اندازه‌ای ثابت برای نام شهر و نام فرد دارید. حال برنامه‌ای بنویسید که این اطلاعات را در زمان اجرا (Runtime) از کاربر دریافت کند.
- برنامه‌ای بنویسید که دو ماتریس را در هم ضرب کند.
- برنامه‌ای بنویسید که یک آرایه را به دو بخش مساوی با در نظر گرفتن تمام حالات ممکن تقسیم کند.
- برنامه‌ای با استفاده از سوئیچ بنویسید که در آن نام یک روز از هفته را از کاربر دریافت کرده و سه حرف اول آن روز را با حروف بزرگ به کاربر نشان دهد.
- یک رشته به عنوان ورودی از کاربر دریافت کرده سپس تعداد حروف تکراری را در خروجی نمایش دهید.
- برنامه‌ای بنویسید که هر عددی را به فرمت باینری تبدیل کند.
- برنامه‌ای بنویسید که یک متن را از یک فایل خوانده، تمام حروف کوچک را به حروف بزرگ و تمام حروف بزرگ را به حروف کوچک تبدیل کند سپس متن تغییر یافته را در خروجی نمایش دهد.
- برنامه‌ای بنویسید که نام، سن، آدرس و نام دانشگاه را از کاربر دریافت کرده و اطلاعات را به او نشان دهد و اگر دوباره نام مشابه‌ای را وارد شد، اطلاعات موجود بازگردانده شوند.

26. انواع حلقه را به همراه سینتکس آن‌ها معرفی کنید.

27. دربارۀ کلیدواژه‌های break و continue در ارتباط با لوپ‌ها چه می‌دانید؟

28. تفاوت میان حلقۀ for و while را بیان کنید و توضیح دهید در چه شرایطی استفاده از یک حلقه نسبت به دیگری برتری دارد؟

29. مفهوم Variable Scope را در جاوا توضیح دهید.

30. مفسر (Interpreter) در جاوا چیست به علاوه اینکه تفاوت کامپایل کردن و تفسیر کردن در جاوا را توضیح دهید.

31. فرض کنید شما باید داده‌ای از جنس عدد صحیح را return کنید اما تایپ خروجی متد یک عدد اعشاری است؛ توضیح دهید آیا در این شرایط کد شما اجرا خواهد شد یا خیر؟

32. آیا می‌توانید متدهای سوپرکلاس و متغیرها را به اصطلاح Override کنید؟

33. منظور از Object Chaining در جاوا چیست؟

34. تفاوت بین آرگومان و پارامتر را در جاوا توضیح دهید.

35. یک کلاس از جنس سینگلتون در زبان جاوا بنویسید و توضیح دهید چه زمانی استفاده از این کلاس مناسب است.

36. از آنجایی که جاوا یک زبان به اصطلاح Multi-thread است، ابتدا این مفهوم را توضیح داده و بیان کنید چرا در توسعهٔ برخی نرم‌افزارها به آن نیاز دارید. همچنین منظور از Thread Sleeping و Thread Pooling را در زبان جاوا توضیح دهید.

37. آیا جاوا یک زبان Procedural است یا Functional و هر کدام از این مفاهیم به چه معنی هستند؟

38. چه پارامترهایی زبان جاوا را از سایر زبان‌های برنامه‌نویسی متمایز می‌کند؟

39. چرا Exception Handling در جاوا معرفی شده است؟

40. فرض کنید در زبان جاوا مکانیسم مدیریت خطاها وجود ندارد؛ با این تفاسیر تابعی بنویسید که به کمک آن بتوانید ارور ArrayIndexOutOfBoundException را مدیریت کنید.

41. تفاوت میان catch ،try و finally را توضیح دهید.

42. بدن خود را به عنوان یک تَسک در نظر بگیرید؛ حال هر یک از اعضای بدن خود را با توجه به مفهوم شییٔ‌گرایی طراحی کنید.
