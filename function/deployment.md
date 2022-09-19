---
layout: default
title: Automated Deployment
parent: Functions
nav_order: 6
---

# Deployment
{: .no_toc }

- TOC
{:toc}

## Workflows (CI/CD)

Function deployments are automated in GitHub Enterprise Server (GHES) using 
CI/CD pipelines with 
[GitHub Actions](https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions). 
Each function app repo will contain the YAML workflows list in the following 
table. These workflows build, test, and deploy the function app's functions, 
and deploy the secrets and app settings. The Test, Pre-Production, and 
Production environments require approval to deploy.

_Note: Reusable workflows stored within a private repository can only 
be used by workflows within the same repository._

| Workflow                          | Reusable  | Description |
| --------------------------------- | --------- | ------ |
| functionapp-build.yaml            | Yes       | A reusable workflow to build and test the function app. | 
| functionapp-deploy.yaml           | Yes       | A reusable workflow to deploy the functions (code). | 
| functionapp-deploy-dev.yaml       | No        | Calls the functionapp-deploy workflow, and deploys the app settings and secrets to the Development environment. |
| functionapp-deploy-promote.yaml   | No        | Calls the functionapp-deploy workflow, and deploys the app settings and secrets to the Test, Pre-Production, and Production environments. An approval is required for each deployment. |

## App Settings

Each environment will have it's own **appsettings.{environemnt}.json** file. 
This file will include all non-secret app settings.

[App settings reference](https://learn.microsoft.com/en-us/azure/azure-functions/functions-app-settings)

``` json
{
    "name": "StorageAccountName",
    "slotSetting": false,
    "value": "stintegrationdev"
}
```

## Secrets

In GitHub, secrets can be found in the repo's **Settings** tab 
under **Security > Actions**. There are three types of actions secrets:

- Environment secrets
- Repository secrets
- Organization secrets

If the function app has secrets, each environment will have it's 
own **secrets.{environment}.json** file. This file will contain an array of 
_secret objects_, where the **appSettingName** value is the name of the app 
setting, and the **secretName** value is the name of the secret.

``` json
{
    "secrets":[
       {
          "appSettingName":"StorageKey",
          "secretName":"<SomeStorageKeySecretName>"
       },
       {
          "appSettingName":"SomeConnectionString",
          "secretName":"<SomeConnectionString>"
       }
    ]
 }
```
