Null check with pattern matching

```csharp
class X {
    public int Value { set;get;}
}

var x = new X { Value = 1 };

if (x is { Value: 1}) {
    Console.WriteLine("Yes");
}

if (x?.Value == 1) {
    Console.WriteLine("Yes");
}


let yesNo = x swith {
	{ Value: 1} => "Yes",
	_ => "No_
};
```