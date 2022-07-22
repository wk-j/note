## Move connection to user secrets

1. Initliaze

```bash
dotnet user-secrets init --project src/RetensionSchedule
```

2. Create secrets file

- `secrets.json`

```json
{
    "ConnectionString": "xyz"
}
```

3. Install secrets into user profile

```bash
cat ./secrets.json | dotnet user-secrets set --project src/RetensionSchedule
```

4. List installed secrets

```bash
dotnet user-secrets list --project src/RetensionSchedule
```

5. Load user secrets into app's configuration

```csharp
builder.Configuration
    .AddJsonFile("_app_/appsettings.json", optional: false, reloadOnChange: true)
    .AddUserSecrets<Program>() // Load user's secrets
    .AddEnvironmentVariables();
```