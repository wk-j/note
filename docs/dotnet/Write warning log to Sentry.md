#sentry #serilog

Install package

```bash
dotnet add package Sentry.Serilog
```

Create logger

```csharp
Log.Logger = new LoggerConfiguration()
	.MinimumLevel.Debug()
	.MinimumLevel.Override("Microsoft", LogEventLevel.Information)
	.Enrich.FromLogContext()
	.WriteTo.Console()
	.WriteTo.File("logs/log-.txt", rollingInterval: RollingInterval.Day)
	.WriteTo.Sentry(opt => {
		opt.Dsn = "https://xyz.ingest.sentry.io/5544660";
		opt.SendDefaultPii = true;
		opt.MinimumBreadcrumbLevel = LogEventLevel.Debug;
		opt.MinimumEventLevel = LogEventLevel.Warning;
		opt.Environment = System.Environment.GetEnvironmentVariable("ASPNETCORE_ENVIRONMENT");
	})
	.CreateLogger();
```