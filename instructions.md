# NBA Data Lake with Azure

## Overview

This repository provides a complete solution for setting up an NBA Data Lake on Microsoft Azure, leveraging Azure Blob Storage, Synapse Analytics, and Python automation. 
It includes scripts to dynamically create Azure resources, fetch NBA data from an API, and store it in a structured data lake.

## Repository Structure
![image](https://github.com/user-attachments/assets/77a58fdc-85fd-48f0-aea9-7e31205c44ea)

🏗️ Azure Services Used

![image](https://github.com/user-attachments/assets/33be52dd-ec0f-4fb7-b3d6-53ebb6d44337)

## 📌 Prerequisites

Ensure you have the following before running the scripts:

### 1️⃣ SportsData.io API Key

Sign up at [SportsData](SportsData.io)

Select NBA as the API you want to use

Copy your API key from the Developer Portal

### 2️⃣ Azure Account (Choose One)

[Azure Free $200 Credit](https://azure.microsoft.com/en-us/pricing/purchase-options/azure-account/search?ef_id=_k_Cj0KCQiA-5a9BhCBARIsACwMkJ67jIcqe3S-QU-D_O1aHxhjC1WkH61u0loQD0H5-tu3OJsRpoy8uz4aAnepEALw_wcB_k_&OCID=AIDcmm5edswduu_SEM__k_Cj0KCQiA-5a9BhCBARIsACwMkJ67jIcqe3S-QU-D_O1aHxhjC1WkH61u0loQD0H5-tu3OJsRpoy8uz4aAnepEALw_wcB_k_&gad_source=1&gclid=Cj0KCQiA-5a9BhCBARIsACwMkJ67jIcqe3S-QU-D_O1aHxhjC1WkH61u0loQD0H5-tu3OJsRpoy8uz4aAnepEALw_wcB)

[Azure for Students](https://azure.microsoft.com/en-us/free/students)

[Azure for Startups](https://www.microsoft.com/en-us/startups)

### 3️⃣ Development Tools

Install VS Code with the following extensions:

Azure CLI Tools

Azure Tools

Azure Resources

### 4️⃣ Install Azure SDK & Python Packages
```
# Install Python (if not installed)
brew install python  # macOS
sudo apt install python3  # Ubuntu/Debian

# Ensure pip is installed
python3 -m ensurepip --default-pip

# Install required Python packages
pip install -r requirements.txt

```

## 🚀 Setup Instructions

### Step 1: Clone the Repository
```
git clone https://github.com/princemaxi/NBA_Datalake-Azure.git
cd NBA_Datalake-Azure
```
###  Step 2: Configure Environment Variables

Create a .env file in the project root and add the following variables:
```
- SportsData.io API Key
SPORTS_DATA_API_KEY=<your_api_key>

- Azure Subscription Details
AZURE_SUBSCRIPTION_ID=<your_subscription_id>
AZURE_RESOURCE_GROUP=<unique_resource_group_name>
AZURE_STORAGE_ACCOUNT=<unique_storage_account_name>
AZURE_SYNAPSE_WORKSPACE=<unique_synapse_workspace_name>

- Leave these blank; they will be populated dynamically
AZURE_CONNECTION_STRING=
AZURE_SYNAPSE_SQL_ENDPOINT=
```

🚨 Note: .env should be added to .gitignore to avoid exposing sensitive credentials.

### Step 3: Run the Setup Script

python setup_nba_data_lake.py

This will:
- ✔️ Create an Azure Storage Account
- ✔️ Create an Azure Blob Container
- ✔️ Configure an Azure Synapse Workspace
- ✔️ Fetch and store NBA data in Blob Storage

### Step 4: Verify Data Upload

- Via Azure Portal
    - Search for the Storage Account in the portal
    - Navigate to Data Storage > Containers
    - Verify that raw-data/nba_player_data.jsonl exists

- Via Azure CLI
    - List blobs in the container
      ```
      az storage blob list \
      --container-name nba-datalake \
      --account-name $AZURE_STORAGE_ACCOUNT \
      --query "[].name" --output table
      ```

    - Download the file
      ```
      az storage blob download \
      --container-name nba-datalake \
      --account-name $AZURE_STORAGE_ACCOUNT \
      --name raw-data/nba_player_data.jsonl \
      --file nba_player_data.jsonl
      ```

    - View the contents
    ```
    cat nba_player_data.jsonl
    ```

## 🎯 What We Learned

- ✅ Creating a data pipeline with Azure Services
- ✅ Automating cloud infrastructure using Python
- ✅ Working with JSON and line-delimited JSONL

## 🔮 Future Enhancements

- 📌 Automate data refresh using Azure Functions
- 📌 Stream real-time NBA data with Azure Event Hubs
- 📌 Build Power BI Dashboards with Synapse Analytics
- 📌 Integrate Azure Key Vault for credential management

### 📜 License

_This project is licensed under the MIT License - see the LICENSE file for details._


