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

#### Answer: 
Abc from B

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

#### Answer: 
str == null <br/>
1/1/0001 12:00:00 AM

Both variables are not initialized, but a string is a reference type and DateTime is a value type. The default value of DateTime type is DateTime.MinValue, which equals 1/1/0001 12:00:00 AM.

</p>
</details>

