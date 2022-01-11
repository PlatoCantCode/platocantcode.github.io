terraform state show

*for the basic terraform state file thats local and in the same folder*
terraform state show terraform

terraform import construction
terraform import {service name}.{human readable name} {Resource ID} 
example:
`terraform import azurerm_key_vault.HRA-KV-ITDevOps /subscriptions/3333333333/resourceGroups/HRA-RG-Networking/providers/Microsoft.KeyVault/vaults/vaultname

variables go in the variables.tf file
comment out the default to prompt the user
variable "Name-ENV" {
 description = "Select: DEV/UAT/PROD"
 default = "DEV"
}


if you want to see  an output add it to the outputs file
output "_instructions" {
 value = "This output contains plain text. You can add variables too."
}

**versions file**
*required for terraform init*

`provider "azurerm" {
 features {}
}
terraform {
 required_providers {
 azurerm = {
 version = "~> 2.83.0"
 }
 }
}`

