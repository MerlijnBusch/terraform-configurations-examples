### RDS Database Configuration Module (rds_instance.tf)

```
# rds_instance.tf

resource "aws_db_instance" "example" {
  allocated_storage    = var.storage_size
  engine               = var.db_engine
  engine_version       = var.engine_version
  instance_class       = var.instance_class
  name                 = var.db_name
  username             = var.db_username
  password             = var.db_password
  parameter_group_name = var.parameter_group_name

  tags = {
    Name = "ExampleDB"
  }
}

```