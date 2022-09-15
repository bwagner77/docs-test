---
layout: default
title: Local Development
parent: Functions
nav_order: 3
---

# Functions Local Development
{: .no_toc }

- TOC
{:toc}

## Environment

- Visual Studio or VS Code
- Azurite (storage emulator)
- Azure Functions Core Tools
- Thunder Client VS Code Extension (optional REST client)

*Note: Some developers have reported issues when attempting to run 
Azure Functions in VS Code (as of 9/14/2022).*

## Developer Guides

[Microsoft Developer Guide](https://docs.microsoft.com/en-us/azure/azure-functions/functions-reference?tabs=blob)
[Quickstart: Create your first C# function in Azure using Visual Studio](https://docs.microsoft.com/en-us/azure/azure-functions/functions-create-your-first-function-visual-studio?tabs=in-process)
[Quickstart: Create a C# function in Azure using Visual Studio Code](https://docs.microsoft.com/en-us/azure/azure-functions/create-first-function-vs-code-csharp?tabs=in-process)
[Quickstart: Create a JavaScript function in Azure using Visual Studio Code](https://docs.microsoft.com/en-us/azure/azure-functions/create-first-function-vs-code-node)

## How to create a new C# Function App in Visual Studio

1. Open Visual Studio 2022 and create a new project using the 
Azure Functions template.

    ![CreateNewProject](../assets/images/function-create-new-project.png)

2. Enter the project name using the following naming convention.

    DH.{Component/Integration}.AzureFunction

    ![ConfigureProject](../assets/images/function-configure-project.png)

3. Select the desired trigger on On the Additional Information screen 
(defaulted to Http trigger).

    ![AdditionalInformation](../assets/images/function-additional-info.png)

4. Your solution's folder structure should look similar to the following.

    ![Structure](../assets/images/function-structure.png)

    [host.json](https://docs.microsoft.com/en-us/azure/azure-functions/functions-host-json)
    : Contains the global configuration options that affect all functions for 
    a function app.

    [local.settings.json](https://docs.microsoft.com/en-us/azure/azure-functions/functions-run-local?tabs=v4%2Cwindows%2Ccsharp%2Cportal%2Cbash#local-settings)
    : Stores the app settings, connection strings, and settings used for local 
    development.
    