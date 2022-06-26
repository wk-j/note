RangeHelper.cs

```csharp
foreach (var i in 10..3) {
    Console.WriteLine(i);
}

public static class RangeHelper {
    public static IEnumerator<int> GetEnumerator(this Range range) {
        var inc = range.Start.Value < range.End.Value ? 1 : -1;
        bool Test(int i) => inc switch { 
			>= 0 => i < range.End.Value, 
			< 0 => i > range.End.Value};
			
        for(int i = range.Start.Value; Test(i); i += inc)
            yield return i;
    }
}
```