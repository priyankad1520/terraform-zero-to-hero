#  Terraform Commands (Step-by-Step )

**1. Install Terraform:** Download from → Terraform official site. Verify installation: Confirms Terraform is installed
```bash
terraform -version
```
**2. Create Project Folder:** Keep all Terraform files in one directory
```bash
mkdir terraform-project
cd terraform-project
```
**3. Create Configuration File:** Create a file:
```bash
touch main.tf
```
`main.tf` → Main configuration file
**4. Write Basic Configuration:** Example (AWS EC2):
```hcl
# Provider (AWS)
provider "aws" {                  
  region = "us-east-1"
}
# Resource (EC2 instance)
resource "aws_instance" "my_ec2" {
  ami           = "ami-12345678"
  instance_type = "t2.micro"
}
```
**5. Initialize Terraform:** Downloads provider plugins, Creates `.terraform/` folder, Prepares environment/working directory
```bash
terraform init    # Must run first time
```
**6. Validate Configuration:** Checks syntax errors, Ensures configuration is correct. Example: Missing brackets → error and Wrong config → error
```bash
terraform validate
```
**7. Format Code (Optional but Good Practice):** Makes code clean and readable/ Cleans and formats your .tf files
```bash
terraform fmt
```
**8. Plan Execution:** What Terraform will create/update/delete, No actual changes yet or “Plan is a dry run”. What resources will be created. What will be changed or destroyed. 
```bash
terraform plan
```
**9. Apply Changes (Create Resources):** Creates infrastructure/ This actually Creates resources in cloud (VM, network, etc.),  Will ask for confirmation → type `yes`.  
```bash
terraform apply
```
**10. Auto Approve (Used in CI/CD):** Skips manual confirmation
```bash
terraform apply -auto-approve
```
**11. Check State:** Shows managed resources/ Shows created resources. 
```bash
terraform state list
```
**12. Show Resource Details:** Displays current infrastructure state/ Track infrastructure in .tfstate file
```bash
terraform show
```
**13. Destroy Resources:** Deletes all created resources created by terraform and it's Saves cost
```bash
terraform destroy
```
**14. Auto Destroy (CI/CD):** 

```bash
terraform destroy -auto-approve
```
**15. Output Values:** Shows outputs like: Public IP, DNS name
```
terraform output
```
---

#### Easy Way to Remember

* **init** → Start
* **validate** → Check
* **plan** → Preview
* **apply** → Create
* **destroy** → Delete
*  “In Terraform, I start with terraform init to initialize, then validate and plan to check changes, and finally apply to create infrastructure. I also use destroy to clean up resources.”
---
#### Terraform Installation Steps
First, configure AWS if needed, then go to the Terraform documentation, download and install Terraform, run the commands on your machine, and finally verify the installation using terraform --version.
1. Step 1: Go to Terraform Official Website
2. Step 2: Choose Your Operating System: Select Windows / Linux / Mac based on your system 
3. Step 3: Download Terraform: Download the Terraform zip file  Extract the file 
4. Step 4: Set Environment Variable (PATH)
-	Copy the Terraform folder path  Add it to System Environment Variables (PATH) 
- This step is important so you can run Terraform from anywhere
5. Step 5: Verify Installation: terraform –version: If installed correctly → it shows Terraform version 
- Download → Extract → Set PATH → Verify using terraform –version
- Basic AWS Configuration (Local System)
- Install AWS CLI → Tool to interact with AWS from terminal 
-	Run aws configure → Start setup process 
-	Enter Access Key → From AWS IAM user 
-	Enter Secret Key → Secure key for authentication 
-	Set Region → Example: ap-south-1 
-	Set Output Format → json (recommended) 
---
#### Terraform Key Terminology 

1. Provider: A plugin that connects Terraform to a cloud platform. “Provider = connection to cloud” Example → AWS, Azure, GCP. Use → Without provider, Terraform cannot create resources 
2. Resource: Actual infrastructure you create. “Resource = what you create” 
Examples → EC2, S3, VPC. Important → Every resource has type + configuration 
3. Module: Reusable Terraform code block. “Module = reusable template” 
Use → Write once, use many times 
Example → Create same EC2 setup for dev & prod 
4. Configuration File (.tf): File where you write Terraform code. “.tf file = where you define everything”. Example files → main.tf, variables.tf, outputs.tf 
5. Variable: Input values for your code. “Variable = dynamic input” 
Example → instance_type = t2.micro. Use → Makes code flexible & reusable 
6. Output: Result shown after execution. “Output = result you see”. Example → EC2 public IP 
7. State File (.tfstate): Stores current infrastructure status. “State = memory of Terraform” 
Why important → Tracks what is created & updated 
8. Plan: Preview of changes. “Plan = what will happen” 
Command → terraform plan. Use → Avoid mistakes before applying 
9. Apply: Executes the changes. “Apply = do the work” 
Command → terraform apply. Result → Resources are created/updated 
10. Workspace: Separate environments. “Workspace = different environments” 
Examples → dev, test, prod. Use → Same code, different environments 
11. Remote Backend: Store state file in remote location. “Remote backend = shared storage” 
Examples → S3, Terraform Cloud. Why needed → Team collaboration + security 
Terraform Lifecycle
•	Write (.tf files) → Define infrastructure in code 
•	terraform init → Initialize project & download providers 
•	terraform validate → Check code syntax 
•	terraform plan → Preview what will be created/changed 
•	terraform apply → Create/update infrastructure 
•	terraform state → Track infrastructure in .tfstate file 
•	terraform destroy → Delete all resources
---
## Conditional Expressions
Conditional expressions in Terraform are used to define conditional logic within your configurations. They allow you to make decisions or set values based on conditions. Conditional expressions are typically used to control whether resources are created or configured based on the evaluation of a condition.
- The syntax for a conditional expression in Terraform is:
- condition ? true_val : false_val
-	condition is an expression that evaluates to either true or false.
-	true_val is the value that is returned if the condition is true.
-	false_val is the value that is returned if the condition is false.
---
## Built-in Functions
Terraform is an infrastructure as code (IaC) tool that allows you to define and provision infrastructure resources in a declarative manner. Terraform provides a wide range of built-in functions that you can use within your configuration files (usually written in HashiCorp Configuration Language, or HCL) to manipulate and transform data. These functions help you perform various tasks when defining your infrastructure. Here are some commonly used built-in functions in Terraform:
1. concat(list1, list2, ...): Combines multiple lists into a single list.
```
variable "list1" {
type    = list
default = ["a", "b"]
}

variable "list2" {
type    = list
default = ["c", "d"]
}

output "combined_list" {
value = concat(var.list1, var.list2)
}
```
2. element(list, index): Returns the element at the specified index in a list.
```
variable "my_list" {
type    = list
default = ["apple", "banana", "cherry"]
}

output "selected_element" {
value = element(var.my_list, 1) # Returns "banana"
}
```
3. length(list): Returns the number of elements in a list.
```
variable "my_list" {
type    = list
default = ["apple", "banana", "cherry"]
}

output "list_length" {
value = length(var.my_list) # Returns 3
}
```
4. map(key, value): Creates a map from a list of keys and a list of values.
```
variable "keys" {
type    = list
default = ["name", "age"]
}

variable "values" {
type    = list
default = ["Alice", 30]
}

output "my_map" {
value = map(var.keys, var.values) # Returns {"name" = "Alice", "age" = 30}
}
```
5. lookup(map, key): Retrieves the value associated with a specific key in a map.
```
variable "my_map" {
type    = map(string)
default = {"name" = "Alice", "age" = "30"}
}

output "value" {
value = lookup(var.my_map, "name") # Returns "Alice"
}
```
6. join(separator, list): Joins the elements of a list into a single string using the specified separator.
```
variable "my_list" {
type    = list
default = ["apple", "banana", "cherry"]
}

output "joined_string" {
value = join(", ", var.my_list) # Returns "apple, banana, cherry"
}
```
These are just a few examples of the built-in functions available in Terraform. You can find more functions and detailed documentation in the official Terraform documentation, which is regularly updated to include new features and improvements

