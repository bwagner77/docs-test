---
layout: default
title: Automated Deployment
parent: Functions
nav_order: 7
---

# Functions Automated Deployment
{: .no_toc }

- TOC
{:toc}

## GitHub Actions (CI/CD)

Functions are deployed in GitHub Enterprise Server (GHES) using 
[GitHub Actions](https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions)
CI/CD pipelines. 
Each function app repo should include the YAML workflows listed in the following 
table. These workflows automate build, test, and deployment of the 
**functions**, **app settings**, and **secrets**. Deploying to the dev 
environment does not require approval. However, deploying to test, pre-prod, 
and prod do require approval.

_Note: 
[Reusable workflows](https://docs.github.com/en/actions/using-workflows/reusing-workflows) 
stored within a private repository can only be used by workflows within the same repository._

| Workflow                          | Reusable  | Description |
| --------------------------------- | --------- | ------ |
| functionapp-build.yaml            | Yes       | A reusable workflow to build and test the function app. | 
| functionapp-deploy.yaml           | Yes       | A reusable workflow to deploy the functions (code). | 
| functionapp-deploy-dev.yaml       | No        | Calls the functionapp-deploy workflow. Also, deploys the app settings and secrets to the Development environment. |
| functionapp-deploy-promote.yaml   | No        | Calls the functionapp-deploy workflow. Also, deploys the app settings and secrets to the Test, Pre-Production, and Production environments. An approval is required for each deployment. |

## App Settings

Each environment will have it's own **appsettings.{environemnt}.json** file. 
This file includes all non-secret app settings. Additional information on 
app settings can be found in the 
[App settings reference](https://learn.microsoft.com/en-us/azure/azure-functions/functions-app-settings).

``` json
{
    "name": "StorageAccountName",
    "slotSetting": false,
    "value": "stintegrationdev"
}
```

## Secrets

A repos ecrets can be found on the GitHub **Settings** tab 
under **Security > Actions**. There are three types of actions secrets:

- Environment secrets
- Repository secrets
- Organization secrets

When a function app has secrets, each environment will have a 
**secrets.{environment}.json** file. This file will contain an array of 
_secret objects_, where the object's **appSettingName** is the name 
of the app setting, and the **secretName** is the name of the secret.

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
