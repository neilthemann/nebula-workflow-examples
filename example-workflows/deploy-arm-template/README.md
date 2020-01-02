# Deploy ARM Template to Azure

This sample workflow deploys resources defined by an Azure Resource Manager template to Azure.

You can deploy any resource that you can with the Azure CLI, this particular example deploys a storage account.

## Prerequisites
Before you run the workflow, you will need to create a Service Pricipal that has Contributor access in your Azure tenant.

You will also need your your Azure Service Principal certificate in PEM format handy.

- More information on creating a Service Principle can be found [here](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?view=azure-cli-latest#create-a-service-principal)

You will also need an ARM template ready to go.
- For further information on creating templates, you can refer to this [tutorial](https://docs.microsoft.com/en-us/azure/azure-resource-manager/templates/template-tutorial-create-first-template?tabs=azure-powershell).

## Run the workflow
Follow these steps to run the workflow:
1. Add your Azure Service Principal PEM certificate block as a secret.
   1. Click **Edit > Secrets.**
   2. Click **Define new secret** and use the following values:
      - **KEY:** cert
      - **VALUE:** Enter your certificate block
      - Your certificate will need to be in PEM format with base64 encoding. It should look similar to this:
      ```
      -----BEGIN PRIVATE KEY-----
      ...
      -----END PRIVATE KEY-----
      -----BEGIN CERTIFICATE-----
      ...
      -----END CERTIFICATE-----
      ```

3. Configure your workflow parameters.
   1. Click **Run** and enter the following parameters:
      - **TenantID:** Your Azure Tenant ID - This can be found under Azure Active Directory > Overview
      - **ApplicationID:** The Application (Client) ID of your Service Principal - This can be found under Azure Active Directory > App Registrations > YourApp > Overview
      - **DeploymentName:** The name for this particular deployment
      - **ResourceGroupName:** The resource group that this deployment will be associated with
      - **templateFilename:** The relative path to the partciular ARM template you want to run within the repository
      - **RepoURL:** The URL to the git repository that contains the ARM template file
      - **StorageAccountName:** The name to use for the storage account. This must be unique and may only contain lowercase letters and numbers. It can be no longer than 24 characters.
      - **gitBranch:** The git branch
    
4. Click **Run workflow** and wait for the workflow run page to appear.

## Check The Deployment Status
1. From the Azure console, under Resource Groups, find the resource group you specified earlier.
2. Select Deployments, you should see the name of the deployment you specified earlier.
3. Under the resource group overview, you should be able to see the deployed resources.

Congratulations! You have deployed a resource to Azure using an ARM template.