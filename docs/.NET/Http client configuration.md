## Preconfig base url and header

```csharp
static class ServiceExtensions {
	private static ServiceCollection AddCustomHttpClient(this IServiceCollection services, AlfrescoOptions options) {
		services.AddHttpClient();

		void Config(HttpClient options) {
			var url = options.Url;
			var user = options.User;
			var password = optionsj.Password;
			var base64 = Convert.ToBase64String(Encoding.ASCII.GetBytes($"{user}:{password}"));

			options.BaseAddress = new Uri(url);
			options.DefaultRequestHeaders.Authorization = 
				new System.Net.Http.Headers.AuthenticationHeaderValue("Basic", base64);
		}
		services.AddHttpClient("alfresco-client")
			.ConfigureHttpClient(Config)
			.ConfigurePrimaryHttpMessageHandler(() => {
				return new HttpClientHandler {
					ServerCertificateCustomValidationCallback =
						HttpClientHandler.DangerousAcceptAnyServerCertificateValidator
				};
			});
			
		return services;
	}
}
```