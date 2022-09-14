---
layout: default
title: Introduction
parent: Azure Functions
grand_parent: Azure
nav_order: 1
---

# Introduction
{: .no_toc }

1. TOC
{:toc}

[Azure Functions] (https://docs.microsoft.com/en-us/azure/azure-functions/)
are a serverless code-first compute service that allow running 
event-triggered code in a scalable way without managing infrastructure.

## Supported Languages

Supported languages: C#, Java, JavaScript, PowerShell, Python

## Use Cases

Note: Designer-first Logic Apps and Power Automate are generally the 
preferred approaches for developing integration and automation services.
A comparison of these services can be found 
[here] (https://docs.microsoft.com/en-us/azure/azure-functions/functions-compare-logic-apps-ms-flow-webjobs?toc=%2Fazure%2Fazure-functions%2Fdurable%2Ftoc.json)

- Build a web API
- Process file uploads
- Respond to database changes
- Run scheduled tasks
- Analyze IoT data streams
- Process data in real time

## Durable Functions

[Durable Functions] (https://docs.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-overview?tabs=csharp) 
are an extension of Azure Functions that let you define 
stateful workflows by writing "orchestrator functions". The state management 
for non-Durable Functions would need to be built manually using queues or 
some other form of Azure Storage. 
