# Azure Web App Deployment with GitHub Actions

This GitHub Actions workflow automates the process of building and deploying a Node.js application to an Azure Web App whenever a commit is pushed to the master branch.

## Prerequisites

- An existing Azure App Service web app. If you haven't created one, follow the guide [here](https://docs.microsoft.com/en-us/azure/app-service/quickstart-nodejs?tabs=linux&pivots=development-environment-cli).
- The repository should contain the Node.js application that you want to deploy.

## Setup

1. **Download the Publish Profile**:  
   From the Overview page of your Web App in the Azure Portal, download the Publish Profile.  
   More details can be found [here](https://docs.microsoft.com/en-us/azure/app-service/deploy-github-actions?tabs=applevel#generate-deployment-credentials).

2. **Add Publish Profile to GitHub Secrets**:  
   In your GitHub repository, create a new secret named `AZURE_WEBAPP_PUBLISH_PROFILE`. Paste the contents of the Publish Profile you downloaded in the previous step as the value.  
   Instructions can be found [here](https://docs.microsoft.com/azure/app-service/deploy-github-actions#configure-the-github-secret).

3. **Configure Environment Variables**:  
   In the workflow file:
   - Set `AZURE_WEBAPP_NAME` to your Azure Web App's name.
   - Optionally, you can modify the `AZURE_WEBAPP_PACKAGE_PATH` if your project is not in the repository root.
   - Optionally, you can set `NODE_VERSION` to the desired version. By default, it's set to version `16.x`.

## Workflow Details

- **Trigger**:  
   The workflow is triggered on a push to the `master` branch or can be dispatched manually.

- **Build Job**:  
   1. Checks out the repository.
   2. Sets up the desired Node.js version.
   3. Installs npm dependencies, builds the application, and runs tests (if they exist).
   4. Uploads the built application as an artifact for the deployment job.

- **Deploy Job**:  
   1. Downloads the built application artifact.
   2. Deploys the application to the Azure Web App using the provided Publish Profile and app name.

## Useful Links

- [GitHub Actions for Azure](https://github.com/Azure/Actions)
- [Azure Web Apps Deploy action](https://github.com/Azure/webapps-deploy)
- [Samples for GitHub Action workflows to deploy to Azure](https://github.com/Azure/actions-workflow-samples)
