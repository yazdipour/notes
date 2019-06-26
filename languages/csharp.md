# CSharp

## Popular QA

* string is alias of System.String (Use String for Class mothods and ref / Use string for Variables)
* `void implClass(string name): base(name){}`  or `void implClass(string name): base(staticFoo(name)){}`
* `bool checkIsPowerOf2(ulong n)=> n!=0 && (n&(n-1)==0);`
* `ref` and `out`: same but `ref` must be init before passing to method.

## Automapper

Just a lib to map object type to another type. ex, `Person {FName, LName, Age} -> Student {FirstName, LName}`

If attributes have same name, it will map automaticlly:

```csharp
Mapper.CreateMap<Person, Student>();
Student st = Mapper.Map<Student>(new Person{FName="",LName=""});
```

else:

```csharp
// Create a map
Mapper.CreateMap<Person, Student>()
.ForMember(dest => dest.FName, opt => opt.MapFrom(src => src.FirstName));
// Use the Map to create obj
Student st = Mapper.Map<Student>(new Person{FName="",LName=""});
```

## Dynamic Type

* A dynamic type escapes type checking at compile time; instead, it resolves type at run time.
* A method can have parameters of the dynamic type.
* The dynamic types do not have intellisense support in visual studio.
* Like variables in JS! They can be anything!

```cs
class X{
    dynamic dynamic_ec = new ExampleClass();
}
```

## Decompile

* https://github.com/0xd4d/de4dot
* https://github.com/0xd4d/dnSpy

## Publish .NetCore App

RuntimeIdentifiers: https://docs.microsoft.com/en-us/dotnet/core/rid-catalog

```powershell
dotnet publish -c Release -r win-x86  (--help)
```

* [خروجی گرفتن از برنامه‌های NET Core 3. بدون وابستگی به فریم‌ورک و در یک فایل Exe](https://www.dotnettips.info/post/3059/خروجی-گرفتن-از-برنامه‌های-net-core-3-بدون-وابستگی-به-فریم‌ورک-و-در-یک-فایل-exe)
* https://www.hanselman.com/blog/MakingATinyNETCore30EntirelySelfcontainedSingleExecutable.aspx
* https://www.hanselman.com/blog/BrainstormingCreatingASmallSingleSelfcontainedExecutableOutOfA

## Extends / Implements

* Java
    ```java
    public class Lion extends Animal implements Diurnal
    ```

* C#
    ```C#
    public class Lion : Animal, // base class must go first
                        Diurnal // then interface(s) if any
    ```

## Abstract

* No impl & must overriden in subclass.
* Can't call `baseClass.abstractFunc()`, Cause there is no impl.

```c#
abstract class absClass{
	public abstract void x();

class implClass : absClass{
	public override void x(){
```

## Virtual

* Can be overriden in subclass / Not forced.

```c#
class MyBaseClass
{
    // virtual auto-implemented property. Overrides can only
    // provide specialized behavior if they implement get and set accessors.
    public virtual string Name { get; set; }

    // ordinary virtual property with backing field
    private int num;
    public virtual int Number
    {
        get { return num; }
        set { num = value; }
    }
}

class MyDerivedClass : MyBaseClass
{
    private string name;

   // Override auto-implemented property with ordinary property
   // to provide specialized accessor behavior.
    public override string Name
    {
```

## Byte[] to String

```csharp
var byteArray = await BlobCache.InMemory.DownloadUrl(App.BASE_URL);
string str = System.Text.Encoding.UTF8.GetString(byteArray);
```

## Fibonacci with Tuples

```csharp
(int current, int previous) Fib(int i){
        if (i == 0) return (1, 0);
        var (p, pp) = Fib(i - 1);
        return (p + pp, p);
}
```

## Check Type and assign

```csharp
switch(shape){
    case Circle c:
        break;
    case Rectangle s when (s.Length == s.Height):
        break;
    case Rectangle r:
        break;
    case null:
        throw new ArgumentNullException(nameof(shape));
}
```

## LINQ

```csharp
list.Find(obj=>obj.Id==Param.Id)

MyList.Select(x=>x.Name).ToArray();

List<Order> SortedList = objListOrder.OrderBy(o=>o.OrderDate).ToList();

//Add all Ienum to ObservableList
IEnum_list.ToList().ForEach(observ_list.Add);
```

## Index

```csharp
var i=^1; //index 1 from last index
"string".SubString(1..^1);
```

## Base64

```csharp
//Encode
public static string Base64Encode(string plainText)
  => return System.Convert.ToBase64String(System.Text.Encoding.UTF8.GetBytes(plainText));

//Decode
public static string Base64Decode(string base64EncodedData)
  => System.Text.Encoding.UTF8.GetString(System.Convert.FromBase64String(base64EncodedData));
```

## Tasks

```csharp
private static string Print(Task<HttpResponseMessage> httpTask)
{
    Task<string> task = httpTask.Result.Content.ReadAsStringAsync();
    string result = string.Empty;
    Task continuation = task.ContinueWith(t =>
    {
        Console.WriteLine("Result: " + t.Result);
        result = t.Result;
    });
    continuation.Wait();  
    return result;
}
```

اگر جایی مجبور شدید از Async استفاده نکنید

بجای

```c#
task.Wait();
var result = task.Result;
```

حتما حتما از روش زیر استفاده کنید

`var result = task.GetAwaiter().GetResult();`

این روش دقیقا مانند روش اول است حتی بحث dead-lock و blocking ترد هم صادق است ولی ...
در روش اول اگر خطایی رخ دهد استثنای صادر شده را در یک AggregateException محصور شده پرتاب میکند که بررسی Detail آن سخت تر و نامفهوم تر است ولی در روش دوم اگر خطایی رخ دهد یک Exception معمولی پرتاب میشود

## Func<T, TResult>

* **Func<TResult\>** — matches a method that takes no arguments, and returns value of type TResuIt.
* **Func<T..., TResult>** — matches a method that takes no argument of type T, and returns value of type TResuIt.

```csharp
Func<int, int> addOne = n => n+1;
Func<int, int, int, > addNums  = (x,y) x + y;
Func<int, bool> isZero = n => n==0;
Console.Write(isZero(addNums ( - 5, 5)));
```

## Action<T\>

Action is like FUNC, but you can't define the returning type. `Action<T> == Func<T>`

```csharp
Action<int, int> addNums = (x,y) => x+y;
```

## Functional

```csharp
bool[] arr={false,true,false};
arr.Count(a=>a==false); //2. Count number of falses
```

## C# 8.0

```csharp
#nullable enable  //to enable roslyn nullable check
class X {
    string? nullableString = null;

    static async Task Main(string[] args){
        var names= GetNames(Service.GetSubscribersAsync());
        await for (var name in names) WriteLine(name);
    }

    static async IAsyncEnumerable<string> GetNames(IAsyncEnumerable<People> people){
        await for (var name in names) yield return GetFirstName(name);
    }

    string foo(Person person)
    {
        return person switch{
            Prof p => $"p {p.name}",
            Student (_, var name)=> $"s name: {name}",
            _ => "z"
        };
    }
}
```

## Switch

```c#
int value = 1;
string greeting = value switch
{
    1 => "hello ",
    2 => "world",
    _ => string.Empty
};

IAnimal animal = new Cat();
string greeting = animal switch
{
    Dog d => $"hello dog {d.Name}",
    Cat c when c.Name == "Lemmy" => $"Hello motorcat!",
    Cat c => $"hello cat {c.Name}",                
    _ => string.Empty
};

void newSwitch(People p){
    return (p.FirstName, p.LastName) switch{
        (null, null)=>"",
        (string f, null)=> $"{f}",
        (string f, string l) => $"{f},{l}",
        (null, string _) => $"{_}"
    };
}
```

## Struct vs Class

* Struct (a value type)
    1. Defining a struct instead of a class if instances of the type are small and commonly short-lived or are commonly embedded in other objects.
    1. **X DO NOT** provide a default constructor for a struct.
    1. **X DO NOT** define mutable value types.
    1. **✓ DO ensure** that a state where all instance data is set to zero, false, or null (as appropriate) is valid.
    1. **✓ DO implement** IEquatable<T> on value types.
    1. **X DO NOT** explicitly extend ValueType. In fact, most languages prevent this.

* Class (a reference type)

* **Differences**
    0. Reference type assignments copy the reference, whereas value type assignments copy the entire value.
    1. Reference types are passed by reference, whereas value types are passed by value.
    2. Reference types are allocated on the heap and garbage-collected, whereas value types are allocated either on the stack or inline in containing types and deallocated when the stack unwinds or when their containing type gets deallocated. Therefore, allocations and deallocations of value types are in general cheaper than allocations and deallocations of reference types.
    3. Arrays of reference types are allocated out-of-line, meaning the array elements are just references to instances of the reference type residing on the heap. Value type arrays are allocated inline, meaning that the array elements are the actual instances of the value type. Therefore, allocations and deallocations of value type arrays are much cheaper than allocations and deallocations of reference type arrays. In addition, in a majority of cases value type arrays exhibit much better locality of reference.
    4. `memory usage`. Value types get boxed when cast to a reference type or one of the interfaces they implement. They get unboxed when cast back to the value type. Because boxes are objects that are allocated on the heap and are garbage-collected, too much boxing and unboxing can have a negative impact on the heap, the garbage collector, and ultimately the performance of the application. In contrast, no such boxing occurs as reference types are cast.

## Boxing

```csharp
int i = 123;
object o = i;   // boxing (Copies the value of i into o)
o = 123;
i = (int)o; // unboxing
```
