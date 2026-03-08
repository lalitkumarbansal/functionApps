# This is my first Function App

## Prerequisites (once per machine)

#### Azure CLI
`az version`
#### Azure Functions Core Tools v4
`func --version`
##### Python (match Azure runtime)
`python --version   # 3.9 / 3.10 / 3.11 recommended`

## Step 1: Create a local project
`mkdir myfuncapp`

`cd myfuncapp`

`func init . --python`

This creates
`host.json`
`local.settings.json`
`requirements.txt`

## Step 2: Create a local python environment

`python -m venv .venv`

`# Windows`

`.venv\Scripts\activate`

`# Linux / macOS`

`source .venv/bin/activate`

## Step 3: Add a function

`func new`

Example:

**Template**: HTTP trigger   
**Function name**: HttpExample   
**Auth level**: anonymous   

## Step 4: Install Dependencies

`pip install requests`

`pip freeze > requirements.txt`

✅ Only requirements.txt is deployed

### Step 5: Exclude venv from deployment (IMPORTANT)

**Create .funcignore:**


`.venv/`

`__pycache__/`

`local.settings.json`

`.git/`

`.vscode/`


This prevents publish failures and bloated packages.

### Step 6: Test Locally

`func start`

**Test**

`curl http://localhost:7071/api/HttpExample`

### Step 7: Login and Select Subscription

`az login`

`az account set --subscription <SUBSCRIPTION_ID>`

### Step 8: Resource Group and Storage Account and Function App


`az group create --name rg-myfunc  --location centralindia`

`az storage account create  --name myfuncstor123   --location centralindia   --resource-group rg-myfunc   --sku Standard_LRS`

` az functionapp create --resource-group rg-myfunc   --consumption-plan-location centralindia  --runtime python  --runtime-version 3.14 --functions-version 4 --name my-python-func-app --storage-account mylalitfuncstor123 --os-type Linux `

**Note**

1) Storage account should be unique
2) Shared Access Key should be Enabled. Query to test the same, outcome must be true. if not Goto Storage Account, Goto Configuration and enable it
   <img width="332" height="74" alt="image" src="https://github.com/user-attachments/assets/050639e4-e715-4430-a626-d57df0f52ce3" />

   ` az storage account show  --name mylalitfuncstor123  --resource-group rg-myfunc --query "allowSharedKeyAccess" `
3) Network should be enabled, Query to test the same

   `az storage account show --name mylalitfuncstor123 --resource-group rg-myfunc --query "networkRuleSet" `

   `az storage account update   --name mylalitfuncstor123   --resource-group rg-myfunc   --bypass AzureServices `
4) 





