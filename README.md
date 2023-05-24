###### 1. What's the output?

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

---
