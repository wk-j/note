
#serilog 

Config

```csharp
public static void Main(string[] args) {
	Log.Logger = new LoggerConfiguration()
		.MinimumLevel.Debug()
		.MinimumLevel.Override("Microsoft", LogEventLevel.Information)
		.MinimumLevel.Override("Microsoft.AspNetCore", LogEventLevel.Warning)
		.Enrich.FromLogContext()
		.WriteTo
			.Logger(c =>
				c.WriteTo
					.Console()
					.Filter.ByExcluding("TypeName = 'Startup'")
			)
		.WriteTo.File("log.txt")
		.CreateLogger();

	CreateHostBuilder(args).Build().Run();
}
```

Usage

```csharp
var world = new {
	Hello = "World"
};

var moon = new {
	Hello = "Moon"
};

var startup = Log.ForContext("TypeName", "Startup");

startup.Information("Hello = {@World}", world);
startup.Information("Hello = {@Moon}", moon);
```