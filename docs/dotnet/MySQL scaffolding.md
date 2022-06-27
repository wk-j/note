## Create main project

```bash
$ dotnet new webapi --output src/MyApp
$ dotnet add src/MyWeb package Microsoft.EntityFrameworkCore.Design
$ dotnet add src/MyWeb pacakge Microsoft.EntityFrameworkCore
$ dotnet add src/MyWeb package Pomelo.EntityFrameworkCore.MySql
```

## Setup user secret

```bash
$ dotnet user-secrets init --project src/MyWeb
$ dotnet user-secrets list --project src/MyWeb
$ cat ./secrets.json | dotnet user-secrets set --project src/MyWeb
```
## Generate models from DB

```bash
$ dotnet ef dbcontext scaffold Name=ConectionStrings \
  	Pomelo.EntityFrameworkCore.MySql \
	-o Models \
	-f \
	-c MyDbContext \
  	-p src/MyWeb
```