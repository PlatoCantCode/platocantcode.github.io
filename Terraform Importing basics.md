General workflow
1. create the resource object in the main.tf file
	this can be as simple as 
	``resource "azurerm_key_vault" "HRA-KV-ITDevOps" 
	{
	
	(resource arguments)
	
	}``

2. run terraform import {service}  {human readable name}   {resource ID}
		review the output and add the required objects into the main.tf file
		or copy from the terraformer .tf file

1. run terraform validate to catch any errors

