# Azure ARM templates to create Network infrastructure

## PROJECT NAME: trees

### Folder network 

This folder include Azure templates t create network infrastructure
2 subnets :
1. for web
2. for DB

web network security groups to let ssh coming from local PC and Internet
db network security groups to let ssh coming from local PC and web subnet

In order to deploy it in stage environment:
using PoerShell
az login
az group create --name rg-tress-stage-westeurope --location westeurope
az deployment group create --resource-group rg-tress-stage-westeurope --template-file .\network\template.json --parameters .\network\stage\parameters.json


### Folder networkWithVms

On top of the network, 2 vms were added each on different subnet

using PoerShell
az login
az group create --name rg-tress-stage-westeurope --location westeurope
$ENV:LINUX_ADMIN_PASSWORD = "azureuser11!"
az deployment group create --resource-group rg-tress-stage-westeurope --template-file .\network\template.json --parameters .\network\stage\parameters.json

coments:
after getting original templates from azure, the below needs to be done:
delete "id" in block "managedDisk" for osDisk and DataDisk

Add adminpassord in "osProfile" block
"adminPassword": "$env:LINUX_ADMIN_PASSWORD",

set "requireGuestProvisionSignal": false in osProfile block
