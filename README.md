<div align="center">
  <img height="120" src="https://play-lh.googleusercontent.com/uGqP7F-E_eaEwTb3hMz63MWf0YKRSK6n9INBwibBSOrGDg6B3sd-ACuqNrR312ohdQ">
  <h1>Curated List of C# Questions & Answers</h1>
</div>

---

###### 1. What's the output?

```cs
class A
{
    public void Abc(int q)
    {
        Console.WriteLine("Abc from A");
    }
}

class B : A
{
    public void Abc(double p)
    {
        Console.WriteLine("Abc from B");
    }
}

static void Main(string[] args)
{
    int i = 5;
    B b = new B();
    b.Abc(i);
}
```

<details><summary><b>Answer</b></summary>
<p>

#### Output: 
Abc from B
#### Explanation: 
Contrary to Java, in C# a class is defined as a component that attempts to be self-sufficient whenever possible. So, the compiler first is looking at the class itself and attempts to resolve a symbol that is requested.

</p>
</details>

---

###### 2. What's the output?

```cs
delegate void SomeMethod();

static void Main(string[] args)
{
    List<SomeMethod> delList = new List<SomeMethod>();
    for (int i = 0; i < 10; i++)
    {
        delList.Add(delegate { Console.WriteLine(i); });
    }

    foreach (var del in delList)
    {
        del();
    }
}
```

<details><summary><b>Answer</b></summary>
<p>

#### Output: 
10  
10  
10  
10  
10  
10  
10  
10  
10  
10

#### Explanation: 
The tricky part here is understanding closures in C#. When the delegate is created, a closure is created, which captures the variable i by reference, not by value. This means that when the delegate is invoked, it will use the value of i at the time of invocation (which is 10), not the value of i at the time the delegate was created. If you wanted each delegate to remember the value of i at the time it was created, you would need to create a temporary variable inside the loop, assign i to it, and use that in the delegate.

</p>
</details>

---

###### 3. What's the output?

```cs
static String str;
static DateTime time;

static void Main(string[] args)
{
    Console.WriteLine(str == null ? "str == null" : str);
    Console.WriteLine(time == null ? "time == null" : time.ToString());
}
```

<details><summary><b>Answer</b></summary>
<p>

#### Output: 
str == null <br/>
1/1/0001 12:00:00 AM
#### Explanation: 
Both variables are not initialized, but a string is a reference type and DateTime is a value type. The default value of DateTime type is DateTime.MinValue, which equals 1/1/0001 12:00:00 AM.

</p>
</details>

---

###### 4. What's the output?

```cs
static void Main(string[] args)
{
    Console.WriteLine(Math.Round(6.5));
    Console.WriteLine(Math.Round(11.5));
}
```

<details><summary><b>Answer</b></summary>
<p>

#### Output: 
6<br/>
12
#### Explanation: 
.NET uses "Banker's Rounding" (also known as "Round Half to Even") as the default rounding mechanism. In this method, if the number to be rounded is exactly halfway between two other numbers, it is rounded to the nearest even number. This method is often used in financial calculations to reduce bias.

</p>
</details>

---

###### 5. What's the output?

```cs
static void Main(string[] args)
{
    string hello = "hello";
    string helloWorld = "hello world";
    string helloWorld2 = "hello world";
    string helloWorld3 = hello + " world";

    Console.WriteLine(helloWorld == helloWorld2);
    Console.WriteLine(object.ReferenceEquals(helloWorld, helloWorld2));
    Console.WriteLine(object.ReferenceEquals(helloWorld, helloWorld3));
}
```

<details><summary><b>Answer</b></summary>
<p>

#### Output: 
True  
True  
False

#### Explanation: 
1. This line checks if the values of helloWorld and helloWorld2 are equal.
2. This line checks if helloWorld and helloWorld2 refer to the exact same object. In C#, the .NET runtime performs a process called string interning for literal strings. This means that when you have two or more identical string literals in your code, the runtime only creates one string object, and all variables that are assigned that string literal actually refer to the same object.
3. In this line, helloWorld3 is created by concatenating hello and " world", which creates a new string object. So even though the value of helloWorld3 is also "hello world", it's not the same object as helloWorld.

</p>
</details>

---

###### 6. What's the output?

```cs
public class TestStatic {
    public static int TestValue;

    public TestStatic() {
        if (TestValue == 0) {
            TestValue = 5;
        }
    }
    static TestStatic() {
        if (TestValue == 0) {
            TestValue = 10;
        }
    }

    public void Print() {
        if (TestValue == 5) {
            TestValue = 6;
        }

        Console.WriteLine("TestValue : " + TestValue);
    }
}

public void Main(string[] args) {
    TestStatic t = new TestStatic();
    t.Print();
}
```

<details><summary><b>Answer</b></summary>
<p>

#### Output: 
TestValue : 10

#### Explanation: 
In C#, a static constructor (also called a type initializer) is called automatically before the first instance is created or any static members are referenced. During the execution of the static constructor, TestValue is 0, so it is set to 10. After that, the instance constructor is run, and than t.Print() is called, but these methods don't change TestValue.

</p>
</details>

---

###### 7. What's the output?

```cs
using System.Threading.Tasks;

public static void Main(string[] args)
{
    Console.WriteLine("Main start");
    Method1();
    Console.WriteLine("Main end");
    Console.ReadLine();
}

public static async void Method1()
{
    Console.WriteLine("Method1 start");
    await Method2();
    Console.WriteLine("Method1 end");
}

public static async Task Method2()
{
    Console.WriteLine("Method2 start");
    await Task.Delay(1000);
    Console.WriteLine("Method2 end");
}
```

<details><summary><b>Answer</b></summary>
<p>

#### Output: 
Main start  
Method1 start  
Method2 start  
Main end  
Method2 end  
Method1 end

#### Explanation: 
The Main method prints "Main start".  
Next, Method1() is called. This is an async method which starts by printing "Method1 start".  
Method1() then calls Method2() using await, meaning it will asynchronously wait for Method2() to complete before it continues. Method2() is an async method that returns a Task. It starts by printing "Method2 start".  
Inside Method2(), we call await Task.Delay(1000). This will pause Method2() for 1 second, during which control is returned back to the calling method.  
Since we are awaiting Method2() in Method1(), control is returned back to the Main method. The "Main end" message is printed.  
The Console.ReadLine() at the end of Main method keeps the program running, which allows us to see the delayed output from the other methods.  
After the delay in Method2(), it prints "Method2 end" and completes.  
Since Method1() was awaiting Method2(), after Method2() completes, control is returned back to Method1() which then prints "Method1 end" and completes.

</p>
</details>

---

###### 8. What's the output?

```cs
class A<T>  
{ 
    static A() 
    { 
        SomeStaticObject = new object(); 
    } 

    public static object SomeStaticObject; 
}

void Main() 
{ 
    Console.WriteLine(Object.ReferenceEquals(A<int>.SomeStaticObject, A<string>.SomeStaticObject)); 
    Console.WriteLine(Object.ReferenceEquals(A<int>.SomeStaticObject, A<int>.SomeStaticObject)); 
} 
```

<details><summary><b>Answer</b></summary>
<p>

#### Output: 
False  
True

#### Explanation: 
The static constructor for `A<int>` is not the same as for `A<string>` because `A<int>` and `A<string>` are considered two different types due to the generic parameters. So, the `SomeStaticObject` of `A<int>` and `A<string>` will be initialized independently, each one will point to a different object.

</p>
</details>

---

###### 9. What's the output?

```cs
using System;
using System.Reflection;

public class Example
{
    public readonly int ReadOnlyField;

    public Example(int value)
    {
        ReadOnlyField = value;
    }
}

public class Program
{
    public static void Main(string[] args)
    {
        Example example = new Example(10);
        Console.WriteLine($"Before applying reflection: {example.ReadOnlyField}");

        // Applying reflection to change the value of readonly field
        var field = typeof(Example).GetField("ReadOnlyField");
        field.SetValue(example, 20);

        Console.WriteLine($"After applying reflection: {example.ReadOnlyField}");
    }
}
```

<details><summary><b>Answer</b></summary>
<p>

#### Output: 
Before applying reflection: 10  
After applying reflection: 20

#### Explanation: 
It's possible to use Reflection to change the value of a `readonly` field, though doing so can lead to unexpected behavior and is generally not recommended as it violates the principle of immutability that `readonly` keyword is meant to enforce.

</p>
</details>

---

###### 10. What's the output?

```cs
var s = new S();

using (s)
{
    Console.WriteLine(s.GetDispose());
}
Console.WriteLine(s.GetDispose());

public struct S : IDisposable
{
    private bool dispose;
    public void Dispose()
    {
        dispose = true;
    }
    public bool GetDispose()
    {
        return dispose;
    }
}
```

<details><summary><b>Answer</b></summary>
<p>

#### Output: 
False  
False

#### Explanation: 
`using` makes a copy of the value type, and you are therefore disposing a copy, not the original. More details: https://ericlippert.com/2011/03/14/to-box-or-not-to-box/

</p>
</details>


