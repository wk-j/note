#serilog

## Enrich with MachineName

Install package

```bash
Serilog.Enrichers.Environment --version 2.2.0-dev-00773
```

Update output template

```csharp
public static void Main(string[] args) {
	Log.Logger = new LoggerConfiguration()
		.MinimumLevel.Debug()
		.MinimumLevel.Override("Microsoft", LogEventLevel.Information)
		.MinimumLevel.Override("Microsoft.AspNetCore", LogEventLevel.Warning)
		.Enrich.FromLogContext()
		.Enrich.WithMachineName()
		.Enrich.WithEnvironmentName()
		.WriteTo.Console(outputTemplate:
			"{Timestamp:HH:mm:ss} [{MachineName}-{EnvironmentName} {Level:u3}] {Message:lj}{NewLine}{Exception}")
		.CreateLogger();

	CreateHostBuilder(args).Build().Run();
}
```

Output

```bash
16:23:35 [iMac-Development INF] Now listening on: https://localhost:5001
16:23:35 [iMac-Development INF] Now listening on: http://localhost:5000
16:23:35 [iMac-Development INF] Application started. Press Ctrl+C to shut down.
16:23:35 [iMac-Development INF] Hosting environment: Development
16:23:35 [iMac-Development INF] Content root path: /Users/wk/Source/serilog/src/Env
```