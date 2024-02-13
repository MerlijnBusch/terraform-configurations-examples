### Example of AWS resource dependency

```
provider "aws" {
  region = "us-west-2"
}

resource "aws_instance" "web_server" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
}

resource "aws_db_instance" "database_server" {
  engine         = "mysql"
  instance_class = "db.t2.micro"
  allocated_storage = 10
}

# Define dependency
depends_on = [
  aws_db_instance.database_server
]
```

With the addition of `depends_on`, we've explicitly stated that the `aws_instance.web_server` resource depends on the `aws_db_instance.database_server` resource. This ensures that Terraform will create the database server before attempting to create the web server.

Now, when you run terraform apply, Terraform will:

1. Create the database server `(aws_db_instance.database_server)`.
2. Once the database server is created, Terraform will then create the web server `(aws_instance.web_server)`.

Conversely, when you run terraform destroy, Terraform will:

1. Destroy the web server `(aws_instance.web_server)`.
2. Once the web server is destroyed, Terraform will then destroy the database server `(aws_db_instance.database_server)`.