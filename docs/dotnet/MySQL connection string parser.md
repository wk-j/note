#mysql

Install package

```
dotnet add package MySql.Data
```

Load connection string

```csharp
class Program {
	static void Main(string[] args) {
		var str = "Port=3306;Host=localhost;User Id=alfresco;Password=password;Database=alfresco";
		var x = new MySql.Data.MySqlClient.MySqlConnectionStringBuilder(str);
		Console.WriteLine($"Database = {x.Database}");
		Console.WriteLine($"Server = {x.Server}");
		Console.WriteLine($"Port = {x.Port}");
		Console.WriteLine($"Password = {x.Password}");
		Console.WriteLine($"User = {x.UserID}");
	}
}
```