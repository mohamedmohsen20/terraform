# Terraform Settings, Providers & Resource Blocks

## Step-02: In c1-versions.tf - Create Terraform Settings Block:
```t 
terraform {
  required_version = "~> 0.14" # which means any version equal & above 0.14 like 0.15, 0.16 etc and < 1.xx
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 3.0" # option but recommended in production
    }
  }
}
```

---------------------------------------------
## Step-03: In c1-versions.tf - Create Terraform Providers Block

### Provider Block
```t 
provider "aws" {
  region  = us-east-1
  profile = "default"
}

```


-------------------------------------------------
## Step-04: In c2-ec2instance.tf - Create Resource Block

```t
# Resource: EC2 Instance
resource "aws_instance" "myec2vm" {
  ami = "ami-0533f2ba8a1995cf9"
  instance_type = "t2.micro"
  user_data = file("${path.module}/2_websetup.sh")
  tags = {
    "Name" = "EC2 Demo"
  }
}
```

## Step-05: Review file 2_websetup.sh
```markdown
#! /bin/bash
# Instance Identity Metadata Reference - https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/instance-identity-documents.html
sudo yum update -y
sudo yum install -y httpd
sudo systemctl enable httpd
sudo service httpd start  
sudo echo '<h1>Welcome to StackSimplify - APP-1</h1>' | sudo tee /var/www/html/index.html
sudo mkdir /var/www/html/app1
sudo echo '<!DOCTYPE html> <html> <body style="background-color:rgb(250, 210, 210);"> <h1>Welcome to Stack Simplify - APP-1</h1> <p>Terraform Demo</p> <p>Application Version: V1</p> </body></html>' | sudo tee /var/www/html/app1/index.html
sudo curl http://169.254.169.254/latest/dynamic/instance-identity/document -o /var/www/html/app1/metadata.html
```