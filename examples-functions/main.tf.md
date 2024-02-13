### Example Functions in terraform

Suppose you have an AWS infrastructure where you want to provision EC2 instances in different AWS regions depending on the environment (e.g., development, staging, production). You want to define a Terraform configuration that automatically selects the appropriate AWS region based on the environment variable provided.

Here's how you can achieve this using Terraform functions and expressions:

```
variable "environment" {
  description = "The environment for the infrastructure (e.g., development, staging, production)"
}

provider "aws" {
  region = lookup({
    "development" = "us-west-2"
    "staging"     = "us-east-1"
    "production"  = "eu-west-1"
  }, var.environment, "us-west-2")
}

resource "aws_instance" "example" {
  ami           = "ami-12345678"
  instance_type = "t2.micro"
  tags = {
    Name = "example-instance"
  }
}
```

In this example:

1. We define a variable named environment to specify the environment (e.g., `development`, `staging`, `production`).
2. We use the `lookup()` function to select the AWS region based on the environment variable provided. If the environment variable doesn't match any of the defined values, it defaults to `"us-west-2"`.
3. The selected AWS region is used to configure the AWS provider.
4. We provision an EC2 instance using the selected AWS region.

With this configuration:

1. If `var.environment` is set to `"development"`, the EC2 instance will be provisioned in the `us-west-2` region.
2. If `var.environment` is set to `"staging"`, the EC2 instance will be provisioned in the `us-east-1` region.
3. If `var.environment` is set to `"production"`, the EC2 instance will be provisioned in the `eu-west-1` region.
4. If `var.environment` is set to any other value, the EC2 instance will be provisioned in the `us-west-2` region by `default`.

### More examples of functions
https://developer.hashicorp.com/terraform/language/functions