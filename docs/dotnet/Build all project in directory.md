## Find and build

```bash
find . -name "*.csproj" | xargs -n1 dotnet build
find . -name "*.csproj" | xargs -n1 dotnet clean
```