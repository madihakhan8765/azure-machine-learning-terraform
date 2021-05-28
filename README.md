# Deploying a Secure Azure Machine Learning Workspace - Terraform Example
This repo shows an example for rolling out a complete Azure Machine Learning enterprise enviroment with network-secured resources via Terraform. This extends the original repo by including network security for all of the workspace dependent resources -- including Azure Container Registry, Azure Storage, and Azure Key Vault. 

This repository includes code for deploying an Azure ML workspace into a standalone, isolated VNET. This can be desirable in cases where you want further isolation from your corporate network or have contstraints on available resources. 

Standalone VNET with workspace and Bastion Jumphost for Client Connectivity
![Deployed resources](media/secure_workspace_with_standalone_vnet.png "Deployed resources")

This includes rollout of the following resources:

* Azure Machine Learning Workspace with Private Link
* Azure Storage Account with VNET binding (using Service Endpoints) and Private Link for Blob and File
* Azure Key Vault with VNET binding (using Service Endpoints) and Private Link
* Azure Container Registry
* Azure Application Insights
* Virtual Network
* Jumphost (Windows) with Bastion for easy access to the VNET
* Compute Cluster (in VNET)
* Compute Instance (in VNET)
* (Azure Kubernetes Service - disabled by default and still under development)

## Instructions

Make sure you have the [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) and the Azure Machine Learning CLI extension installed (`az extension add -n azure-cli-ml`).

1. Copy `terraform.tfvars.example` to `terraform.tfvars`
1. Update `terraform.tfvars` with your desired values
2. Run Terraform
    ```console
    $ terraform init
    $ terraform plan
    $ terraform apply
    ```

If you want to deploy AKS, you need to have [Azure Machine Learning CLI installed](https://docs.microsoft.com/en-us/azure/machine-learning/reference-azure-machine-learning-cli).

# Known Limitations

* Still need to update `Default Datastore` to use Managed Identity of the Studio UI data access

# Important Notes

* The user fileshare for the Compute Instances will be automatically provisioned upon first instance access