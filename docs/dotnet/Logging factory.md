## Install

```
$ dotnet pacakge src/MyApp package Microsoft.Extensions.Logging.Console
```


## Logging factory

```csharp
var logging = LoggerFactory.Create(builder => builder.AddConsole());
var builder = new DbContextOptionsBuilder<MyDbContext>()
	.UseLoggerFactory(logging)
	.UseNpgsql("Host=;User Id=;Password=;Databse=;");
```