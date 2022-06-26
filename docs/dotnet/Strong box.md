Instead of doing this

```csharp
object value = 100;
int i = (int) value
```

Use StrongBox

```csharp
var box = new StringBox(100);
int value = box.Value;
```

Reference

- https://github.com/dotnet/runtime/discussions/47774