# Azure Blob Storage Static Website Setup

This document outlines the steps to configure a static website on Azure Blob Storage using the provided template files from `oxer.zip`.

## Prerequisites

- Azure CLI installed on your machine.
- An Azure account with appropriate permissions.
- `oxer.zip` template downloaded.

## Steps to Setup

### 1. Extract and Prepare Template Files

After downloading `oxer.zip`, extract its contents:

```bash
unzip oxer.zip -d oxer-template
cd oxer-template
2. Azure CLI Steps
2.1 Ensure You're Logged Into Azure
Log into your Azure account using the following command:

bash
Copy code
az login
2.2 Create a Resource Group (if not already done)
Create a new resource group to hold your storage account:

bash
Copy code
az group create --name storagedemo --location eastus
2.3 Create a Storage Account
Create a new storage account with the desired configurations:

bash
Copy code
az storage account create --name ltdeepstoredemo --resource-group storagedemo --location eastus --sku Standard_RAGRS --kind StorageV2 --min-tls-version TLS1_2 --allow-blob-public-access false
3. Enable Static Website Hosting
Set up the storage account to serve as a static website:

bash
Copy code
az storage blob service-properties update --account-name ltdeepstoredemo --static-website --index-document index.html --404-document 404.html
4. Upload Template Files
Navigate to the template directory and upload the files to the $web container:

bash
Copy code
az storage blob upload-batch --destination '$web' --source . --account-name ltdeepstoredemo
5. Get the Static Website URL
Retrieve the URL of the static website:

bash
Copy code
az storage account show --name ltdeepstoredemo --query "primaryEndpoints.web" --output tsv
6. Access the Website
Open the retrieved URL in your browser to view the deployed site.

Conclusion
You have successfully set up a static website on Azure Blob Storage using the oxer template