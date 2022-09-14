---
layout: default
title: Infrastructure
parent: Azure Functions
grand_parent: Azure
nav_order: 2
---

# Infrastructure
{: .no_toc }

1. TOC
{:toc}

[placeholder] Function Apps run within an App Service Enviornment (ASE). An 
ASE is an App Service feature that provides a fully isolated and dedicated 
enviornment for securely running App Service apps at high scale.

Cold start is a non-issue when running within an ASE/decidated host.

## Service Limits

A more complete list of service limits can be found 
[here](https://docs.microsoft.com/en-us/azure/azure-functions/functions-scale) 

| Default timeout duration  | 30 minutes    |
| Max instance count        | 100           |
| Max request size          | 100 MB        |
| Max query string length   | 4096          |
| Max request URL length    | 8192          |
