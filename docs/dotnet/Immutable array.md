## Do not initialize with `new` keyword

```csharp
class Program {
	static void X(ImmutableArray<int> x) {
		Console.WriteLine(x.IsDefault); // true
		Console.WriteLine(x == null);   // true

		// error CS0037
		// Console.WriteLine(x is null);
	}

	static void Main(string[] args) {
		ImmutableArray<int> x = new();
		X(x);
	}
}
```