## `ExceptionDispatchInfo`

```csharp
static void Error() {
	var list = new List<Exception>();
	try {
		var k = 0;
		var x = 100 / k;
	} catch (Exception ex) {
		list.Add(ex);
	}

	if (list.Any()) {
		ExceptionDispatchInfo.Capture(list[0]).Throw();
	}
}
```