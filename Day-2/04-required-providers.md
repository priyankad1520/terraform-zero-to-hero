# Provider Configuration
1. required_providers → Defines which provider + version Terraform should download. Install provider (what + version). required_providers is used to define provider source and version 

2. provider block → Defines how to use/configure the provider. Open app and set language/login. provider block is used to configure provider settings like region, credentials

- The required_providers block in Terraform is used to declare and specify the required provider configurations for your Terraform module or configuration. It allows you to specify the provider name, source, and version constraints.
#### Provider Configuration
```
terraform {   # Define global Terraform configuration block
  required_providers {   # Declare all required providers for this project
   
 aws = {   # Configure AWS provider
      source  = "hashicorp/aws"   # Download AWS provider from HashiCorp registry
      version = "~> 3.0"   # Use version >=3.0 and <4.0 (compatible versions)
    }

    azurerm = {   # Configure Azure provider
      source  = "hashicorp/azurerm"   # Download Azure provider from HashiCorp registry
      version = ">= 2.0, < 3.0"   # Use version between 2.0 and less than 3.0
    }
  }
}
```
#### Quick Understanding 
-	terraform → Main configuration block 
-	required_providers → List of providers Terraform must install 
-	aws / azurerm → Provider names 
-	source → Where Terraform downloads provider 
-	version → Controls which versions are allowed 
#### --> Why we use this: Avoid version conflicts, Ensure same setup in all environments, Control provider updates and Support multi-cloud (AWS + Azure)
