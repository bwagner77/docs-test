---
layout: default
title: Local Development
parent: Functions
nav_order: 4
---

# Functions Local Development
{: .no_toc }

- TOC
{:toc}

## Environment

Function are developed locally in Visual Studio using Azure Functions Core Tools.

- Microsoft Windows
- Visual Studio or VS Code
- Azurite (storage emulator)
- Azure Functions Core Tools
- Thunder Client, VS Code Extension REST client (optional)

*Note: Some developers have reported issues when trying to run Functions 
in VS Code (as of 9/14/2022).*

## How to create a new C# Function App in Visual Studio

1. Open Visual Studio 2022 and create a new project using the 
**Azure Functions** template.

    ![CreateNewProject](../assets/images/function-create-new-project.png)

2. Enter a **Project name** using the following naming convention.

    DH.{Component/Integration}.AzureFunction

    ![ConfigureProject](../assets/images/function-configure-project.png)

3. On the Additional Information screen selected the desired trigger 
(defaulted to Http trigger).

    ![AdditionalInformation](../assets/images/function-additional-info.png)

4. Your solution's folder structure should look similar to the following.

    ![Structure](../assets/images/function-structure.png)

    [host.json](https://docs.microsoft.com/en-us/azure/azure-functions/functions-host-json)
    : Lets you configure the Functions host. These settings apply both when 
    running locally and in Azure.

    [local.settings.json](https://docs.microsoft.com/en-us/azure/azure-functions/functions-run-local?tabs=v4%2Cwindows%2Ccsharp%2Cportal%2Cbash#local-settings)
    : Stores the app settings and connection strings used for local 
    development.

5. Open the function file (BusinessFunction.cs). The **FunctionName** attribute 
for Run indicates the method is the entry point for the function.

    ``` csharp
    public static class BusinessFunction
    {
        [FunctionName("BusinessFunction")]
        public static async Task<IActionResult> Run(
            [HttpTrigger(AuthorizationLevel.Function, "get", "post", Route = null)] HttpRequest req,
            ILogger log)
        {
            log.LogInformation("C# HTTP trigger function processed a request.");

            string name = req.Query["name"];

            string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
            dynamic data = JsonConvert.DeserializeObject(requestBody);
            name = name ?? data?.name;

            string responseMessage = string.IsNullOrEmpty(name)
                ? "This HTTP triggered function executed successfully. Pass a name in the query string or in the request body for a personalized response."
                : $"Hello, {name}. This HTTP triggered function executed successfully.";

            return new OkObjectResult(responseMessage);
        }
    }
    ```

6. Press F5 to start the function in debug mode. You might be prompted to 
enable Windows firewall exception.

    ![FunctionDebugConsole](../assets/images/function-debug-console.png)

7. Test executing the function using cURL or with Thunder Client 
VS Code extension.

    ![FunctionRunCurl](../assets/images/function-run-curl.png)

    ![FunctionRunThunderClient](../assets/images/function-run-thunderclient.png)

## Additional developer guides

[Microsoft Developer Guide](https://docs.microsoft.com/en-us/azure/azure-functions/functions-reference?tabs=blob)
[Quickstart: Create your first C# function in Azure using Visual Studio](https://docs.microsoft.com/en-us/azure/azure-functions/functions-create-your-first-function-visual-studio?tabs=in-process)
[Quickstart: Create a C# function in Azure using Visual Studio Code](https://docs.microsoft.com/en-us/azure/azure-functions/create-first-function-vs-code-csharp?tabs=in-process)
[Quickstart: Create a JavaScript function in Azure using Visual Studio Code](https://docs.microsoft.com/en-us/azure/azure-functions/create-first-function-vs-code-node)