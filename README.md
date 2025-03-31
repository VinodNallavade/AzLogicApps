# Logic App Consumption Plan Deployment

This repository contains an Azure Resource Manager (ARM) template for deploying a Logic App (Consumption plan).

## Prerequisites

Before deploying the Logic App, ensure you have the following:

* **Azure Subscription:** An active Azure subscription.
* **Azure CLI or PowerShell:** Installed and configured with your Azure account.
* **ARM Template:** The ARM template file (e.g., `logic-app.json`) containing the Logic App definition.
* **Parameters File (Optional):** A parameters file (e.g., `logic-app.parameters.json`) if you need to customize the deployment.

## Deployment Steps

1.  **Clone the Repository (Optional):**

    If you have this README and the template files in a repository, clone it to your local machine:

    ```bash
    git clone <repository_url>
    cd <repository_folder>
    ```

2.  **Review the ARM Template:**

    Examine the `logic-app.json` file to understand the resources being deployed. Pay attention to the parameters, variables, and resources defined in the template.

3.  **Create or Review the Parameters File (Optional):**

    If you have a `logic-app.parameters.json` file, review and modify it to match your desired configuration. If you don't have one, you can create it or pass parameters directly during deployment.

    Example `logic-app.parameters.json`:

    ```json
    {
      "$schema": "[https://schema.management.azure.com/schemas/2019-04-01/deploymentParameters.json#](https://www.google.com/search?q=https://schema.management.azure.com/schemas/2019-04-01/deploymentParameters.json%23)",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "logicAppName": {
          "value": "MyLogicApp"
        },
        "location": {
          "value": "eastus"
        },
        "connectionName":{
          "value": "MyConnection"
        },
        "connectionResourceId": {
          "value": "/subscriptions/YOUR_SUBSCRIPTION_ID/resourceGroups/YOUR_RESOURCE_GROUP/providers/Microsoft.Web/connections/YOUR_CONNECTION_NAME"
        }
        //Add any additional parameters here.
      }
    }
    ```

    **Important:** Replace `YOUR_SUBSCRIPTION_ID`, `YOUR_RESOURCE_GROUP`, and `YOUR_CONNECTION_NAME` with your actual Azure resource IDs.

4.  **Deploy the Logic App using Azure CLI:**

    Use the following Azure CLI command to deploy the Logic App:

    ```bash
    az deployment group create \
      --resource-group <resource_group_name> \
      --template-file logic-app.json \
      --parameters @logic-app.parameters.json #If you are using parameters file.
      #or pass parameters inline
      #--parameters logicAppName=MyLogicApp location=eastus connectionName=MyConnection connectionResourceId="/subscriptions/YOUR_SUBSCRIPTION_ID/resourceGroups/YOUR_RESOURCE_GROUP/providers/Microsoft.Web/connections/YOUR_CONNECTION_NAME"
    ```

    Replace `<resource_group_name>` with the name of the resource group where you want to deploy the Logic App. If the resource group doesn't exist, it will be created.

5.  **Deploy the Logic App using PowerShell:**

    Use the following PowerShell command to deploy the Logic App:

    ```powershell
    New-AzResourceGroupDeployment `
      -ResourceGroupName <resource_group_name> `
      -TemplateFile logic-app.json `
      -TemplateParameterFile logic-app.parameters.json #If you are using parameters file.
      #or pass parameters inline
      #-logicAppName "MyLogicApp" -location "eastus" -connectionName "MyConnection" -connectionResourceId "/subscriptions/YOUR_SUBSCRIPTION_ID/resourceGroups/YOUR_RESOURCE_GROUP/providers/Microsoft.Web/connections/YOUR_CONNECTION_NAME"
    ```

    Replace `<resource_group_name>` with the name of the resource group.

6.  **Verify the Deployment:**

    After the deployment is complete, verify that the Logic App has been created successfully in the Azure portal or using the Azure CLI/PowerShell.

    **Azure CLI:**

    ```bash
    az logicapp show --resource-group <resource_group_name> --name <logic_app_name>
    ```

    **PowerShell:**

    ```powershell
    Get-AzLogicApp -ResourceGroupName <resource_group_name> -Name <logic_app_name>
    ```

## Post-Deployment Configuration

* Configure the Logic App triggers and actions as needed.
* Set up any required connections and authentication.
* Monitor the Logic App's performance and logs.

## Contributing

Feel free to contribute to this repository by submitting pull requests or opening issues.

## License

[Add your license here]
