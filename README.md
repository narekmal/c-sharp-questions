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

###### 3. What's the output?

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

###### 4. What's the output?

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

