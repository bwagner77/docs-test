---
layout: default
title: Functions Runtimes and Languages
parent: Functions
nav_order: 3
---

# Runtimes and Languages
{: .no_toc }

- TOC
{:toc}

## Runtimes

The following table lists recent Azure Functions runtime host versions.

The runtime version used by published apps in Azure is dictated by 
the FUNCTIONS_EXTENSION_VERSION 
[app setting](https://docs.microsoft.com/en-us/azure/azure-functions/functions-app-settings#functions_worker_runtime){:target="_blank"}.

| Version   | App Setting Value   | Support Level | Description | 
| --------- | ------------------- | ------------- | ----------- |
| 4.x       | ~4                  | GA            | Recommended runtime version for functions in all languages. Use this version to run C# functions on .NET 6.0 and .NET 7.0 | 
| 3.x       | ~3                  | GA            | Supports all languages. Use this version to run C# functions on .NET Core 3.1 and .NET 5.0. | 

The TargetFramework and AzureFunctionsVersion are found in the C# project 
file (.csproj).

*See the Languages table below for compatibility.*

``` xml
<PropertyGroup>
  <TargetFramework>net6.0</TargetFramework>
  <AzureFunctionsVersion>v4</AzureFunctionsVersion>
</PropertyGroup>
```

## Languages

All functions in a function app must share the same langauge. The langauge 
for a function app is stored in the FUNCTIONS_WORKER_RUNTIME app setting.

| Language      | 3.x                       | 4.x | 
| ------------- | ------------------------- | ---------------------------- |
| C#            | .NET Core 3.1, .NET 5.0   | .NET 6.0, .NET 7.0 (Preview) | 
| JavaScript    | Node.js 10, 12, 14        | Node.js 14, 16, 18 (Preview) | 
| F#            | .NET Core 3.1             | .NET 6.0 | 
| Java          | Java 8, 11                | Java 8, 11 | 
| Python        | 3.6, 3.7, 3.8, 3.9        | 3.7, 3.8, 3.9 | 

## Extension Bundles

Extension bundles are a way to add a pre-defined compatible set of binding 
extensions to a non-.NET function app. Each extension bundle version contains 
a specific set of binding extensions that are verified to work together.

Starting with version 4.x, the Functions runtime enforces a minimum 
extension version for all trigger and binding extensions. Additional details 
can be found in the 
[Microsoft Docs](https://docs.microsoft.com/en-us/azure/azure-functions/functions-versions?tabs=azure-cli%2Cin-process%2Cv4&pivots=programming-language-csharp#minimum-extension-versions){:target="_blank"}

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
