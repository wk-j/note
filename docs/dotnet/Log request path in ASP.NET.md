#serilog 

## Setup

Program.cs

```csharp
public static void Main(string[] args) {
	Log.Logger = new LoggerConfiguration()
		.MinimumLevel.Debug()
		.MinimumLevel.Override("Microsoft", LogEventLevel.Information)
		.MinimumLevel.Override("Microsoft.AspNetCore", LogEventLevel.Warning)
		.Enrich.FromLogContext()
		.WriteTo.Console()
		.CreateLogger();

	CreateHostBuilder(args).Build().Run();
}
```

Startup.cs

```csharp
app.UseSerilogRequestLogging();
```

Output

```log
[12:33:51 INF] Now listening on: https://localhost:5001
[12:33:51 INF] Now listening on: http://localhost:5000
[12:33:51 INF] Application started. Press Ctrl+C to shut down.
[12:33:51 INF] Hosting environment: Development
[12:33:51 INF] Content root path: /Users/wk/Source/serilog/src/Http
[12:33:55 INF] HTTP POST /api/hello/updateMessage responded 200 in 81.5256 ms
[12:34:01 INF] HTTP POST /api/hello/updateMessage responded 200 in 1.3437 ms
[12:34:04 INF] HTTP POST /api/hello/updateMessage responded 200 in 0.9602 ms
```