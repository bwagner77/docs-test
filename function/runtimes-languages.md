---
layout: default
title: Runtimes and Languages
parent: Functions
nav_order: 3
---

# Functions Runtimes and Languages
{: .no_toc }

- TOC
{:toc}

## Runtimes

The following table lists the latest Azure Functions runtime host versions. 
The runtime version used in Azure is dictated by the 
FUNCTIONS_EXTENSION_VERSION 
[app setting](https://docs.microsoft.com/en-us/azure/azure-functions/functions-app-settings#functions_worker_runtime).

| Version   | App Setting Value   | Support Level | Description | 
| --------- | ------------------- | ------------- | ----------- |
| 4.x       | ~4                  | GA            | Recommended version for all languages. Use this version to run C# functions on .NET 6.0 and .NET 7.0 | 
| 3.x       | ~3                  | GA            | Supports all languages. Use this version to run C# functions on .NET Core 3.1 and .NET 5.0 | 

The TargetFramework and AzureFunctionsVersion settings are found in the C# 
project file (.csproj).

*See the Languages table below for compatibility.*

``` xml
<PropertyGroup>
  <TargetFramework>net6.0</TargetFramework>
  <AzureFunctionsVersion>v4</AzureFunctionsVersion>
</PropertyGroup>
```

## Languages

All functions in a function app must share the same language. The language 
for a function app is stored in the FUNCTIONS_WORKER_RUNTIME setting.

| Language      | 3.x                       | 4.x | 
| ------------- | ------------------------- | ---------------------------- |
| C#            | .NET Core 3.1, .NET 5.0   | .NET 6.0, .NET 7.0 (Preview) | 
| JavaScript    | Node.js 10, 12, 14        | Node.js 14, 16, 18 (Preview) | 
| F#            | .NET Core 3.1             | .NET 6.0 | 
| Java          | Java 8, 11                | Java 8, 11 | 
| Python        | 3.6, 3.7, 3.8, 3.9        | 3.7, 3.8, 3.9 | 

## Extension bundles

Extension bundles are a way to add a pre-defined compatible set of binding 
extensions to a non-.NET function app. Each version of an extension bundle 
contains a specific set of binding extensions that are verified to work 
together.

Starting with version 4.x, the Functions runtime enforces a minimum 
extension version for all trigger and binding extensions. Additional details 
can be found in the 
[Microsoft Docs](https://docs.microsoft.com/en-us/azure/azure-functions/functions-versions?tabs=azure-cli%2Cin-process%2Cv4&pivots=programming-language-csharp#minimum-extension-versions)

The extension bundle reference can be found in the **host.json** file.

``` json 
{
    "version": "2.0",
    "extensionBundle": {
        "id": "Microsoft.Azure.Functions.ExtensionBundle",
        "version": "[2.*, 3.0.0)"
    }
}
```
## .NET isolated process

Previously functions only supported a tightly integrated mode for .NET 
functions by running as a *class library* in the same process as the host. 
This mode has deep integration between the host process and functions. 

With the .NET isolated process functions run *out-of-process*. This 
decouples the code from the runtime, thus eliminating assembly version 
conflicts between the app and the host process. A .NET isolated function 
project is basically a .NET console app that targets a supported .NET runtime. 
When functions run out-of-process, the .NET project uses a unique set of 
packages, which implement both core functionality and binding extensions.

See the 
[Microsoft Docs](https://docs.microsoft.com/en-us/azure/azure-functions/dotnet-isolated-process-guide)
for additional information.
