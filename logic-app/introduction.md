---
layout: default
title: Introduction
parent: Logic Apps
nav_order: 1
---

# Logic Apps Introduction
{: .no_toc }

- TOC
{:toc}

## What is an Azure Logic App?

[Azure Logic Apps](https://learn.microsoft.com/en-us/azure/logic-apps/)
is a designer-first cloud-based platform for creating and running 
automated workflows that integrate apps, data, services, and systems. 
As a member of Azure Integration Services, you can quickly develop highly 
scalable integration solutions for your enterprise and 
business-to-business (B2B) scenarios.

## Common use cases

When compared to functions, logic apps are better suited for integrations 
as many connectors are available out of the box. A comparison between 
functions and Logic Apps can be found in the 
[Microsoft Docs](https://learn.microsoft.com/en-us/azure/azure-functions/functions-compare-logic-apps-ms-flow-webjobs).

The following are some common use cases:

- Integration between Azure cloud services
- SaaS event processing
- Timer-based and content-based triggers
- Data ingestion and transformation
- Business processes

## Standard vs. Consumption

Azure offers two Logic App resource types; Standard (single-tenant) 
and Consumption (multi-tenant). Data Hub exclusively uses 
Logic Apps (Standard) running inside an App Service Environment (ASE) as it 
provides the following benefits:

- Fully isolated
- Integrated support for VNETs and private endpoints
- Resource sharing - can run multiple workflows in the same Logic App
- More control and capabilities around runtime and performance settings
- Better deployment process as the infrastructure can be separated 
from the app
- Allows for both stateful and stateless workflows
- VS Code support for local development

See the 
[Microsoft Docs](https://learn.microsoft.com/en-us/azure/logic-apps/single-tenant-overview-compare) 
for a detailed comparison of Standard vs. Consumption 

## Anatomy of a Logic App

| Term      | Description | 
| --------- | ----------- |
| Workflow  | A workflow is a series of steps that defines a task or process. Each workflow starts with a single trigger, followed by one or more actions. |
| Trigger   | A trigger is always the first step in any workflow and specifies the condition for running any further steps in that workflow. |
| Action    | An action is a step in a workflow after the trigger. Every action runs some operation in a workflow. | 

A logic apps infrastructure and code are defined in 
[ARM Templates](https://learn.microsoft.com/en-us/azure/azure-resource-manager/templates/overview). 
The underlying workflow code/logic is defined in a _workflow definition_. 
The workflow definition uses JSON and follows a structure that's validated 
by the 
[Workflow Definition Language](https://learn.microsoft.com/en-us/azure/logic-apps/logic-apps-workflow-definition-language)
schema.

## Comparing stateful and stateless workflows

The following is a comparison of stateful and stateless worfklow types. 
Only **stateful** workflows should be used in Data Hub. 

**Important**: Once a workflow has been created, the type cannot be changed.

| Feature                                   | Stateful                      | Stateless | 
| ----------------------------------------- | ----------------------------- | -- |
| Stores run history, inputs, and outputs   | Yes                           | No | 
| Managed connectors allowed                | Yes                           | No | 
| Supports unit testing                     | Yes                           | No |
| Supports chunking                         | Yes                           | No | 
| Supports asynchronous operations          | Yes                           | No | 
| Max run duration                          | Variable                      | Best for runs less than 5 minutes | 
| Message handling                          | Can handle large messages     | Best for handling small messages under 64 KB | 
