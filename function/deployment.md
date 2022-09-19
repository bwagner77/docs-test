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
CI/CD pipelines with GitHub Actions. Each function app repo will contain the 
YAML workflows list in the following table. These workflows build, test, 
and deploy the function app's functions, and deploy the secrets and 
app settings.

_Note: Reusable workflows stored within a private repository can only 
be used by workflows within the same repository._

| Workflow                          | Reusable  | Description |
| --------------------------------- | --------- | ------ |
| functionapp-build.yaml            | Yes       | A reusable workflow to build and test the function app. | 
| functionapp-deploy.yaml           | Yes       | A reusable workflow to deploy the functions (source). | 
| functionapp-deploy-dev.yaml       | No        | Calls functionapp-deploy workflow, and deploys the app settings with secrets to the Development environment. |
| functionapp-deploy-promot.yaml    | No        | Calls functionapp-deploy workflow, and deploys the app settings with secrets to the Test, Pre-Production, and Production environments. An approval is required for each deployment. |

## App Settings

Each environment will have it's own appsettings.{environemnt}.json file. This
file will include all non-secret app settings.

``` json
{
    "name": "StorageAccountName",
    "slotSetting": false,
    "value": "stintegrationdev"
}
```

## Secrets

If the function app has secrets, each environment will have it's 
own secrets.{environment}.json file. This file contains an array of objects, 
where the value of **appSettingName** will be the app setting name, 
and the value of **secretName** will be the name of the secret.

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
