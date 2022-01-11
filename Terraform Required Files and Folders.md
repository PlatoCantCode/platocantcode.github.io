Key files required to run Terraform init
1. main.tf
This is your main file that defines the resources your going to create or manage within Terraform.
[See TF Example Main.tf](obsidian://open?vault=MainVault&file=Notes%2FTerraform%2FTerraform%20Examples%2FTF%20Example-Main.tf)

2. outputs.tf
We declare what we want to get back from the terraform providers once the state has been applied
[See TF Example-Outputs.tf](obsidian://open?vault=MainVault&file=Notes%2FTerraform%2FTerraform%20Examples%2FTF%20Example-Outputs.tf).

3. variables.tf
Define what variables you'll be calling in the main.tf file
[See TF Example-Variables.tf](obsidian://open?vault=MainVault&file=Notes%2FTerraform%2FTerraform%20Examples%2FTF%20Example-Variables.tf).

4. providers.tf
This is where we define what providers we're going to use and what terraform version to run against.
Note that this changed in version 0.14 so you may need to update code to reflect this.
[See TF Example-Providers](obsidian://open?vault=MainVault&file=Notes%2FTerraform%2FTerraform%20Examples%2FTF%20Example-Providers-TFversion0.14).

5. README.md
Just in case you want to post on github or whatever. You can add other non-TF files to the folder.


Example:
Folder Structure

Terraform-Project Folder
```hcl
.
├── main.tf
├── outputs.tf
├── README.md
├── providers.tf
└── variables.tf
└── MODULES
	└──SUBNET
		├── main.tf
		├── outputs.tf
		└── variables.tf
```

