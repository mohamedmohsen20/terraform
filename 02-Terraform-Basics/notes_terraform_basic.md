***02-01-Install-Tools-TerraformCLI***

- Install Terraform CLI
    Linux --------> https://www.terraform.io/downloads
          --------> https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli#install-cli
- Install AWS CLI


---------------------------------
***02-02-Terraform-Command-Basics****

Understand basic Terraform Commands:
$ terraform init
$ terraform validate
$ terraform plan
$ terraform apply
$ terraform destroy


*** 02-03-Terraform-Language-Syntax ***

Understand Blocks:

# Template
<BLOCK TYPE> "<BLOCK LABEL>" "<BLOCK LABEL>"   {
  # Block body
  <IDENTIFIER> = <EXPRESSION> # Argument
}

# AWS Example
resource "aws_instance" "ec2demo" {
    # BLOCK body
  ami           = "ami-04d29b6f966df1537" # Argument
  instance_type = var.instance_type # Argument with   value as expression (Variable value replaced from varibales.tf
}



***Understand about Terraform Top-Level Blocks***

- Terraform Settings Block
- Provider Block
- Resource Block
- Input Variables Block
- Output Values Block
- Local Values Block
- Data Sources Block
- Modules Block
