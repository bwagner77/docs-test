---
layout: default
title: Introduction
parent: Azure Functions
grand_parent: Azure
nav_order: 1
---

# Introduction
{: .no_toc }

[Azure Functions](https://docs.microsoft.com/en-us/azure/azure-functions/)
are a serverless code-first compute service that allow running 
event-triggered code in a scalable way without managing infrastructure. A 
function is invoked by a *trigger* and executes a block of code or 
or business logic.

- TOC
{:toc}

## Languages and Supported Runtimes for 4.x

| Language      | Runtimes for 4.x      |
| :------------ | :-------------------- |
| C#            | .NET 6.0              |
| JavaScript    | Node 14, 16           |
| Java          | Java 8, 11            |
| Python        | Python 3.7, 3.8, 3.9  |

## Common Use Cases

**Note**: Logic Apps (designer-first) and Power Automate are typically 
preferred approaches when developing integration and automation services. 
A comparison of these services can be found 
[here](https://docs.microsoft.com/en-us/azure/azure-functions/functions-compare-logic-apps-ms-flow-webjobs?toc=%2Fazure%2Fazure-functions%2Fdurable%2Ftoc.json).

- Computing backend calculations
- File processing
- Respond to database changes
- Run scheduled tasks
- Data stream processing
- Analyze IoT data streams
- Lightweight web APIs

## Durable Functions

[Durable Functions](https://docs.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-overview?tabs=csharp) 
are an extension of Azure Functions that let you define stateful workflows by 
writing "orchestrator functions".

## Triggers and Bindings

Functions are invoked by a *trigger* and can have exactly one. In addition 
to invoking the function, certain triggers can also serve as bindings. Bindings 
provide a declarative way to connect data to your code. They can be passed 
in (input) or receive data (output).