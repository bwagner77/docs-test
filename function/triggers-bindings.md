---
layout: default
title: Triggers and Bindings
parent: Functions
nav_order: 3
---

# Functions Triggers and Bindings
{: .no_toc }

- TOC
{:toc}

## Triggers

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

## Bindings

A binding is a connection to data within a function. Bindings may be connected 
as input bindings, output bindings, or both. Data from bindings is provided 
to the function as parameters. All bindings, except for HTTP and timer triggers, 
must be explicitly added to the function app project.

Additional information for triggers and bindings can be found in the 
[Microsoft Docs](https://learn.microsoft.com/en-us/azure/azure-functions/functions-triggers-bindings?tabs=csharp).
