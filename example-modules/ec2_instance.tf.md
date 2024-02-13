### EC2 Instance Configuration Module (ec2_instance.tf):

```
# ec2_instance.tf

resource "aws_instance" "example" {
  ami           = var.ami_id
  instance_type = var.instance_type
  key_name      = var.key_name

  tags = {
    Name = "ExampleInstance"
  }
}
```