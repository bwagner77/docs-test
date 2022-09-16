---
layout: default
title: Add Dependency Injection
parent: Code Samples
grand_parent: Functions
nav_order: 1
---

# Add Dependency Injection
{: .no_toc }

See the 
[Microsoft Docs](https://docs.microsoft.com/en-us/azure/azure-functions/functions-dotnet-dependency-injection)
for further information on function dependency injection.

*Note: This custom dependency injection model does not apply to .NET 
isolated functions. The .NET isolated process model relies on regular 
ASP.NET Core dependency injection patterns.*

## Prerequisites

- Visual Studio or VS Code
- Microsoft.Azure.Functions.Extensions
- Microsoft.NET.Sdk.Functions
- Microsoft.Extensions.DependencyInjection

## 1. Register services

Add a new class named **Startup.cs** to your functions project. Create a 
method for configuring and adding components to an IFunctionsHostBuilder 
instance.  

Add **FunctionsStartup** assembly attribute to specify the type name 
used during startup.

``` csharp
using Microsoft.Azure.Functions.Extensions.DependencyInjection;
using Microsoft.Extensions.Configuration;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Logging;

[assembly: FunctionsStartup(typeof(DH.Integration.AzureFunction.Startup))]

namespace DH.Integration.AzureFunction
{
    public class Startup : FunctionsStartup
    {
        public override void Configure(IFunctionsHostBuilder builder)
        {
            builder.Services.AddHttpClient();
        }

        public override void ConfigureAppConfiguration(IFunctionsConfigurationBuilder builder)
        {
            var context = builder.GetContext();

            builder.ConfigurationBuilder
                .SetBasePath(context.ApplicationRootPath)
                .AddJsonFile("local.settings.json", optional: true, reloadOnChange: true)
                .AddEnvironmentVariables()
                .Build();
        }
    }
}
```

## 2. Use injected dependencies in the function

Constructor injection is used to make dependencies available in a 
function. Notice both the class and Run method were made **non-static**.

``` csharp
namespace DH.Integration.AzureFunction
{
    public class BusinessFunction
    {
        private readonly HttpClient _httpClient;

        public BusinessFunction(HttpClient httpClient)
        {
            _httpClient = httpClient;
        }

        [FunctionName("BusinessFunction")]
        public async Task<IActionResult> Run(
            [HttpTrigger(AuthorizationLevel.Function, "get", "post", Route = null)] HttpRequest req,
            ILogger log)
        {
            var response = await _httpClient.GetAsync("https://microsoft.com");

            return new OkObjectResult("Response from function with injected dependencies.");
        }
    }
}
```
