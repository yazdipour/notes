# CSharp

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

## Return Switch (C# 7.2 or 8)

```csharp
string foo(Person person)
{
    return person switch{
        Prof p => $"p {p.name}",
        Student (_, var name)=> $"s name: {name}",
        _ => "z"
    };
}
```

## Base64

```csharp
//Encode
public static string Base64Encode(string plainText) {
  var plainTextBytes = System.Text.Encoding.UTF8.GetBytes(plainText);
  return System.Convert.ToBase64String(plainTextBytes);
}

//Decode
public static string Base64Decode(string base64EncodedData) {
  var base64EncodedBytes = System.Convert.FromBase64String(base64EncodedData);
  return System.Text.Encoding.UTF8.GetString(base64EncodedBytes);
}
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

## Func Delegates

* **Func<TResult\>** — matches a method that takes no arguments, and returns value of type TResuIt.
* **Func<T, TResult>** — matches a method that takes no argument of type T, and returns value of type TResuIt.

```csharp
Func<int, int> addOne = n => n+1;
Func<int, int, int, > addNums  = (x,y) x + y;
Func<int, bool> isZero = n => n==0;
Console. ( isZero( addNums ( - 5, 5)));

```

## Functional

```csharp
bool[] arr={false,true,false};
arr.Count(a=>a==false); //2. Count number of falses
```