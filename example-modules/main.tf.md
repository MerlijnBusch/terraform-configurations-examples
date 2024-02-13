### Main Terraform Configuration File (main.tf)

```
# main.tf

module "ec2_instance" {
  source = "./ec2_instance"
  ami_id = var.ec2_ami_id
  instance_type = var.ec2_instance_type
  key_name = var.ec2_key_name
}

module "rds_instance" {
  source = "./rds_instance"
  storage_size = var.rds_storage_size
  db_engine = var.rds_engine
  engine_version = var.rds_engine_version
  instance_class = var.rds_instance_class
  db_name = var.rds_db_name
  db_username = var.rds_db_username
  db_password = var.rds_db_password
  parameter_group_name = var.rds_parameter_group_name
}

module "iam_role" {
  source = "./iam_role"
}
```

In this example, each Terraform module (`ec2_instance.tf`, `rds_instance.tf`, `iam_role.tf`) encapsulates the configuration for a specific type of resource. The main Terraform configuration file (`main.tf`) then imports these modules and passes necessary variables to configure them. This approach allows for better organization, reuse, and maintainability of Terraform configurations.