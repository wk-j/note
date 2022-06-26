#csharp

## Convert DateTime to ISO 8601


```csharp
var date = DateTime.Now;

Console.WriteLine(date.ToString("o"));
Console.WriteLine(date.ToUniversalTime().ToString("o"))
```

Output

```bash
2021-01-21T15:50:49.9400000+07:00
2021-01-21T08:50:49.9400000Z
```
