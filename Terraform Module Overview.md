TF Modules are a collection of config files that all do *one task.*
This is the key foundation for being able to reuse code.
Look at this terragrunt output. 


```bash

└── azurerm
    ├── analysis
    │   ├── analysis.tf
	│	├── provider.tf
    │   ├── terraform.tfstate
    │   └── variables.tf
    |── data_factory
    │   ├── data_factory.tf
    │   ├── data_factory_integration_runtime_azure.tf
    │   ├── outputs.tf
    │   ├── provider.tf
    │   ├── variables.tf

```

This tool produces modules based on whats already in your azure resource groups. 
The items that already have a .tfstate are because terragrunt imported the objects into the statefile. Anything that already has a state file can be seen with:

```hcl
terraform show
```


Recap:
Modules are folders that contain the following:
	providers 
	variables
	outputs 
	module_name.tf
	
The module_name.tf is just like your main.tf file.
Its what resources your going to manage.

##### Writing a module - "Subnet"
General work flow for me is to write the provider, then main module. And while I write the main module, add in the variables and end with the desired output file.

provider.tf
```hcl
provider "azurerm" {
  features {}
}
```



[main.tf](https://github.com/Azure/terraform-azurerm-network/blob/master/main.tf)


```hcl
\\\fetch the resource group name from our var file

data "azurerm_resource_group" "network" {
    name = var.resource_group_name
	location = var.location
}

data "azurerm_virtual_network" "vnet_name" {
    name = var.vnet
}

resource "azurerm_subnet" "subnet" {
   count = length(var.subnet_names)
   name = var.subnet_names[count.index]
   resource_group_name = data.azurerm_resource_group.network.name
   address_prefixes = [var.subnet_prefixes[count.index]]
   virtual_network_name = azurerm_virtual_network.vnet.name
}

 depends_on = [azurerm_resource_group.network]

```
This is just a rough model of a module.
You can pull the real files from the [azure github](https://github.com/Azure/terraform-azurerm-network).






----------------
[variables.tf](https://github.com/Azure/terraform-azurerm-network/blob/master/variables.tf)
```hcl
  
variable "location" {
 description = "The region where the virtual network is created."
 default = "eastus"
 }

variable "vnet" {
     description = "Name of the main vNet we're working within"
     type = string
     default = "vNet01"
}

\\vnet info
variable "address_space" 
{
	description = "The address space that is used by the virtual network."
	type = string
	default = "10.105.0.0/16"
}
\\vnet info
variable "address_spaces" {
	description = "The list of the address spaces that is used by the virtual network."
	type = list(string)
	default = ["10.0.0.0/16"]
}

variable "subnet_names" {
	description = "The names of subnets"
	type = list(string)
	default = ["subnet1","subnet2"]
}

variable "subnet_prefixes" {
	description = "The address prefix to use for the subnet."
	type = list(string)
	default = ["10.0.1.0/24", "10.0.2.0/24", "10.0.3.0/24"]
}
```
Note how the location var is not in our variables.tf file
This is because we're going to define that globally on the parent variable file and we want this to be flexible yet consistent. 

----------------
[output.tf](https://github.com/Azure/terraform-azurerm-network/blob/master/outputs.tf)
```hcl
output "vnet_address_space" {
description = "The address space of the vNet"
value = azurerm_virtual_network.vnet.address_space
}

output "vnet_subnets" {
description = "The ids of subnets created inside the newly created vNet"
value = azurerm_subnet.subnet.*.id
}

output "azurerm_resource_group" {
description = "The name of which resource group this was created in"
value = azurerm_resource_group.name
}
```

	
##### How to call modules

Write the block within your *parent* main.tf file to call the desired module
So your final main.tf will look like this.

```hcl

resource "azurerm_resource_group" "JG-RG-Network" {
  name     = "JG-RG-Network"
  location = "${var.location}"
}

module "subnet" {
  source              = "./"
  resource_group_name = azurerm_resource_group.JG-RG-Network.name
  address_spaces      = ["10.0.0.0/16", "10.2.0.0/16"]
  subnet_prefixes     = ["10.0.1.0/24", "10.0.2.0/24", "10.0.3.0/24"]
  subnet_names        = ["subnet1", "subnet2", "subnet3"]
  }
  
depends_on = [azurerm_resource_group.JG-RG-Network]
```


#### Conclusion
Build modules only when they are a collection of steps.
For example, in the real world. A subnet in azure requires a vnet, subnet, resource group. BUT, there's often other required items, security group baselines,  tags, blueprint's to apply. But lumping all your 'subnet' actions together in the module. You can ensure that the tags, NSG's and other required items are created whenever you build a new subnet.


-----------


##### Remote Modules - For building on the shoulders of giants

**Github**
```hcl
 source  = "git@github.com:your-organization/the-repository-name.git?ref=1.0.0"
```

**Terraform also has a public modules in the Terraform Registry**
[Official Microsoft Azure Hashicorp Registry](https://registry.terraform.io/namespaces/Azure)
```hcl
 source  = "Azure/network/azurerm"
```


##### Sources:


[Official Microsoft Azure Hashicorp Registry](https://registry.terraform.io/namespaces/Azure)

[General Hashicorp Registry](https://registry.terraform.io)

[What are Terraform Modules](https://spacelift.io/blog/what-are-terraform-modules-and-how-do-they-work)

[Hashicorp Official Tutorial](https://www.terraform.io/docs/language/modules/index.html)
