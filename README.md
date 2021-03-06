# GitHub Action for building Azure Web Apps

![V1_BuildAndDeploy_PythonApp_ToAzureWebApp](https://github.com/MicrosoftOryx/githubactions-samples/workflows/V1_BuildAndDeploy_PythonApp_ToAzureWebApp/badge.svg?branch=master)
![V1_BuildAndDeploy_PhpApp_ToAzureWebApp](https://github.com/MicrosoftOryx/githubactions-samples/workflows/V1_BuildAndDeploy_PhpApp_ToAzureWebApp/badge.svg?branch=master)
![V1_BuildAndDeploy_NodeApp_ToAzureWebApp](https://github.com/MicrosoftOryx/githubactions-samples/workflows/V1_BuildAndDeploy_NodeApp_ToAzureWebApp/badge.svg?branch=master)
![V1_BuildAndDeploy_AspNetCoreApp_ToAzureWebApp](https://github.com/MicrosoftOryx/githubactions-samples/workflows/V1_BuildAndDeploy_AspNetCoreApp_ToAzureWebApp/badge.svg?branch=master)
![V2Beta_BuildAndDeploy_PythonApp_ToAzureWebApp](https://github.com/MicrosoftOryx/githubactions-samples/workflows/V2Beta_BuildAndDeploy_PythonApp_ToAzureWebApp/badge.svg?branch=master)
![V2Beta_BuildAndDeploy_NodeApp_ToAzureWebApp](https://github.com/MicrosoftOryx/githubactions-samples/workflows/V2Beta_BuildAndDeploy_NodeApp_ToAzureWebApp/badge.svg?branch=master)
![V2Beta_BuildAndDeploy_AspNetCoreApp_ToAzureWebApp](https://github.com/MicrosoftOryx/githubactions-samples/workflows/V2Beta_BuildAndDeploy_AspNetCoreApp_ToAzureWebApp/badge.svg?branch=master)

With the Azure App Service Actions for GitHub, you can automate your workflow to deploy [Azure Web Apps](https://azure.microsoft.com/en-us/services/app-service/web/) using GitHub Actions.

Get started today with a [free Azure account](https://azure.com/free/open-source)!

This repository contains the GitHub Action for [building Azure Web Apps on Linux](./action.yml) using the [Oryx](https://github.com/microsoft/Oryx) build system. Currently, the following platforms can be built using this GitHub Action:

- .NET Core
- Node
- PHP
- Python

If you are looking for a GitHub Action to deploy your Azure Web App, consider using [`azure/webapps-deploy`](https://github.com/Azure/webapps-deploy).

The definition of this GitHub Action is in [`action.yml`](./action.yml).

Now we have a beta version [`v2-beta`](https://github.com/Azure/appservice-build/tree/v2-beta) released. It's using a [`new image specifically for GitHub Actions`](https://github.com/microsoft/Oryx/blob/master/images/build/GitHubActions.Dockerfile
) to significantly reduce the time for building your app.

# End-to-End Sample Workflows

## Dependencies on other GitHub Actions

- [`actions/checkout`](https://github.com/actions/checkout)
  - Checkout your Git repository content into the GitHub Actions agent

## Other GitHub Actions

- [`azure/webapps-deploy`](https://github.com/Azure/webapps-deploy)
  - Deploy a web app to Azure

### Sample workflow to build a web app

The following is a sample of a workflow that builds a web app in a repository whenever a commit is pushed:

```
on: push

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Cloning repository
        uses: actions/checkout@v1

      - name: Building web app
        uses: azure/appservice-build@v1
```

### Sample workflow to build and deploy an Azure Web App

The following is a sample workflow that builds a web app in a repository and then deploys it to Azure whenever a commit is pushed:

```
on: push

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Cloning repository
        uses: actions/checkout@v1

      - name: Building web app
        uses: azure/appservice-build@v1

      - name: Deploying web app to Azure
        uses: azure/webapps-deploy@v1
        with:
          app-name: <WEB_APP_NAME>
          publish-profile: ${{ secrets.AZURE_WEB_APP_PUBLISH_PROFILE }}
```
