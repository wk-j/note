Statup

```csharp
using System;
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Hosting;
using Microsoft.EntityFrameworkCore;
using Microsoft.Extensions.Configuration;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;

namespace Mg {
    public class Startup {
        public Startup(IConfiguration configuration) {
            Configuration = configuration;
        }

        public IConfiguration Configuration { get; }

        public void ConfigureServices(IServiceCollection services) {
            const string cc = ***REMOVED***;

            services.AddDbContext<KpiEntity.KpiContext>(options => {
                options.UseNpgsql(cc, v => {
                    v.MigrationsAssembly("KpiMigration");
                    // v.SetPostgresVersion(9, 4);
                });
            });
            services.AddControllers();
        }

        public void Configure(IApplicationBuilder app, IWebHostEnvironment env) {
            if (env.IsDevelopment()) {
                app.UseDeveloperExceptionPage();
            }

            app.UseHttpsRedirection();
            app.UseRouting();
            app.UseAuthorization();
            app.UseStaticFiles();
            app.UseEndpoints(endpoints => endpoints.MapControllers());
        }
    }

    class Program {
        public static void Main(string[] args)
             => CreateHostBuilder(args).Build().Run();

        public static IHostBuilder CreateHostBuilder(string[] args) =>
            Host.CreateDefaultBuilder(args)
                .ConfigureWebHostDefaults(
                    webBuilder => webBuilder.UseStartup<Startup>());
    }
}
```

Addition package

```xml
  <ItemGroup>
    <PackageReference Include="Microsoft.EntityFrameworkCore.Design" Version="5.0.2">
      <IncludeAssets>runtime; build; native; contentfiles; analyzers; buildtransitive</IncludeAssets>
      <PrivateAssets>all</PrivateAssets>
    </PackageReference>
    <PackageReference Include="Microsoft.Extensions.DependencyInjection" Version="5.0.1" />
    <PackageReference Include="Npgsql.EntityFrameworkCore.PostgreSQL" Version="5.0.2" />
  </ItemGroup>
```

Generate SQL

```bash
dotnet ef migrations script     	--project src/Mg -o  sql/X3.sql
```

Add migration

```bash
dotnet ef migrations add init   	--project src/Mg
dotnet ef migrations add xyz 		--project src/Mg
```

Remove migration

```bash
dotnet ef migrations remove   		--project src/Mg
```

Update or drop  ⭐️

```
dotnet ef database update			--project src/Mg
dotnet ef database drop             --project src/Mg
```