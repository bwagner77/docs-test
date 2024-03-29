---
layout: default
title: Introduction
parent: Functions
nav_order: 1
---

# Functions Introduction
{: .no_toc }

- TOC
{:toc}

## What is an Azure Function?

[Azure Functions](https://learn.microsoft.com/en-us/azure/azure-functions/)
are a serverless code-first compute service that allow running 
event-triggered code in a scalable way without managing infrastructure. A 
function is invoked by a *trigger* and executes a block of code or 
business logic.

## Common use cases

Logic Apps (designer-first) and Power Automate are generally the preferred 
approaches when developing integration and automation services. 
Azure Functions is a serverless compute service, whereas Azure Logic Apps 
is a serverless workflow integration platform. A comparison between 
functions and Logic Apps can be found in the 
[Microsoft Docs](https://learn.microsoft.com/en-us/azure/azure-functions/functions-compare-logic-apps-ms-flow-webjobs).

The following are some common use cases:

- Computing backend calculations
- File processing
- Respond to database changes
- Run scheduled tasks
- Data stream processing
- Analyze IoT data streams
- Lightweight web APIs

## Durable Functions

[Durable Functions](https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-overview?tabs=csharp)
are an extension of Azure Functions that let you define stateful workflows by 
writing "orchestrator functions".

## Triggers and bindings

A trigger defines how a function is invoked. Triggers have associated data,
which is often provided as the payload of the function.  The following 
are some common triggers:

| Trigger               | Description   | 
| --------------------- | ------------- | 
| Timer trigger         | Called on a predefined schedule. |
| Blob trigger          | Fired when a new or updated blob is detected. |
| Event Hub trigger     | Fired when events are delivered to an Azure Event Hub. |
| HTTP trigger          | Fired from a HTTP request | 
| Queue trigger         | Fired when any new messages arrive in an Azure Storage Queue. | 
| Service Bus trigger   | Fired when a new message comes from a service bus queue or topic | 

A binding is a connection to data within a function. Bindings may be connected 
as input bindings, output bindings, or both. Data from bindings is provided 
to the function as parameters. All bindings, except for HTTP and timer triggers, 
must be explicitly added to the function app project.

Additional information for triggers and bindings can be found in the 
[Microsoft Docs](https://learn.microsoft.com/en-us/azure/azure-functions/functions-triggers-bindings?tabs=csharp).
