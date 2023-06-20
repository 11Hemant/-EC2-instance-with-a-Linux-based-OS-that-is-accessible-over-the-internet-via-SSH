# -EC2-instance-with-a-Linux-based-OS-that-is-accessible-over-the-internet-via-SSH

## Step 1:Create a new file called main.tf and add the following code:

provider "aws" {
  region = var.region
}

resource "aws_instance" "example_instance" {
  ami           = "our_ami_id"
  instance_type = var.instance_type
  key_name      = var.key_name
  subnet_id     = var.subnet_id
  vpc_security_group_ids = [var.security_group_id]

  tags = {
    Name = "ExampleInstance"
  }
}

output "InstanceId" {
  value = aws_instance.example_instance.id
}

output "PublicIpAddress" {
  value = aws_instance.example_instance.public_ip
}

## Step 2:Create a new file called variables.tf and add the following code:

variable "region" {
  description = "AWS region where the instance will be deployed"
  type        = string
}

variable "key_name" {
  description = "Name of the SSH key to be installed on the instance"
  type        = string
}

variable "instance_type" {
  description = "EC2 instance type"
  type        = string
}

variable "subnet_id" {
  description = "ID of the subnet where the instance will be deployed"
  type        = string
}

variable "security_group_id" {
  description = "ID of the security group for the instance"
  type        = string
}
## Step 3:Replace the placeholder values:

Replace our_ami_id with the ID of the Linux-based AMI we want to use (e.g., Amazon Linux 2).
In the variables.tf file, we'll define the values for the input variables region, key_name, instance_type, subnet_id, and security_group_id during runtime.

## Step 4:Save both the main.tf and variables.tf files.

## Step 5:Open a terminal or command prompt, navigate to the directory containing the Terraform files, and run the following commands:


terraform init

terraform plan

terraform apply

## Step 6:Terraform will initialize, show us the execution plan, and prompt for confirmation. Review the plan and type yes to proceed.

## Step 7:Wait for Terraform to create the EC2 instance. Once the process is complete, Terraform will display the output, including the instance ID and public IP address.

## Step 8:we  have now an EC2 instance with a Linux-based OS that is accessible over the internet via SSH. The instance ID and public IP address are available as outputs. Yowe can use the public IP address to connect to the instance using SSH.
