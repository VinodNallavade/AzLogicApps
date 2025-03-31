# Logic App Deployment (HTTP Trigger Response)

This repository contains an Azure Resource Manager (ARM) template for deploying a simple Logic App (Consumption plan) that responds to HTTP requests with a "Hello from Logic App!" message.

## Prerequisites

Before deploying the Logic App, ensure you have the following:

* **Azure Subscription:** An active Azure subscription.
* **Azure CLI or PowerShell:** Installed and configured with your Azure account.

## Deployment Steps

1.  **Clone the Repository (Optional):**

    If you have this README and the template file in a repository, clone it to your local machine:

    ```bash
    git clone <repository_url>
    cd <repository_folder>
    ```

2.  **Review the ARM Template:**

    Examine the `logic-app.json` file to understand the resources being deployed. This template creates a Logic App with an HTTP request trigger and a response action.

3.  **Deploy the Logic App using Azure CLI:**

    Use the following Azure CLI command to deploy the Logic App:

    ```bash
    az deployment group create \
      --resource-group <resource_group_name> \
      --template-file logic-app.json \
      --parameters logicAppName=<logic_app_name> location=<azure_region>
    ```

    * Replace `<resource_group_name>` with the name of the resource group where you want to deploy the Logic App. If the resource group doesn't exist, it will be created.
    * Replace `<logic_app_name>` with the name you want to give your Logic App.
    * Replace `<azure_region>` with the Azure region where you want to deploy the Logic App (e.g., `eastus`, `westus2`, `uksouth`).

4.  **Deploy the Logic App using PowerShell:**

    Use the following PowerShell command to deploy the Logic App:

    ```powershell
    New-AzResourceGroupDeployment `
      -ResourceGroupName <resource_group_name> `
      -TemplateFile logic-app.json `
      -logicAppName <logic_app_name> `
      -location <azure_region>
    ```

    * Replace `<resource_group_name>` with the name of the resource group.
    * Replace `<logic_app_name>` with the name of the logic app.
    * Replace `<azure_region>` with the azure region.

5.  **Retrieve the HTTP Trigger URL:**

    After the deployment is complete, you need to retrieve the HTTP trigger URL to invoke your Logic App.

    **Azure CLI:**

    ```bash
    az logicapp show --resource-group <resource_group_name> --name <logic_app_name> --query "endpointsConfiguration.workflow.endpoints.accessEndpoints[?name=='When_a_HTTP_request_is_received'].value" -o tsv
    ```

    **PowerShell:**

    ```powershell
    (Get-AzLogicApp -ResourceGroupName <resource_group_name> -Name <logic_app_name>).EndpointsConfiguration.Workflow.Endpoints.AccessEndpoints | Where-Object {$_.Name -eq "When_a_HTTP_request_is_received"} | Select-Object -ExpandProperty Value
    ```

    Replace `<resource_group_name>` and `<logic_app_name>` with your actual values.

6.  **Test the Logic App:**

    Use a tool like `curl`, Postman, or a web browser to send an HTTP request to the retrieved URL. You should receive a response with the message "Hello from Logic App!".

    **Example using `curl`:**

    ```bash
    curl <http_trigger_url>
    ```

## Post-Deployment Configuration

* You can modify the Logic App definition in the `logic-app.json` file to add more complex actions and logic.
* You can add authorization to your http trigger.
