### Here's an example of how you can use variables in Terraform to parameterize configurations and outputs:

```
# Define variables
variable "instance_type" {
  description = "The type of EC2 instance to launch"
  default     = "t2.micro"
}

variable "region" {
  description = "The AWS region where resources will be provisioned"
  default     = "us-east-1"
}

# AWS provider configuration
provider "aws" {
  region = var.region
}

# Create an EC2 instance
resource "aws_instance" "example" {
  ami           = "ami-12345678"
  instance_type = var.instance_type
}

# Output the public IP address of the instance
output "instance_public_ip" {
  description = "The public IP address of the EC2 instance"
  value       = aws_instance.example.public_ip
}
```

In this example:

1. We define two variables: `instance_type` and `region`. These variables allow us to specify the type of EC2 instance and the AWS region where resources will be provisioned, respectively. The description field provides context for each variable, and the default field specifies a default value that will be used if not overridden.

2. The AWS provider configuration section uses the region variable to specify the region where resources will be provisioned.

3. The `aws_instance` resource block creates an EC2 instance. We use the `instance_type` variable to specify the instance type.

4. The `output` block defines an output variable named `instance_public_ip`, which exposes the public IP address of the EC2 instance.