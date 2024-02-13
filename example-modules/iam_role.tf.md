### IAM Role Configuration Module (iam_role.tf):

```
resource "aws_iam_role" "example" {
  name = "ExampleRole"

  assume_role_policy = jsonencode({
    Version = "2012-10-17"
    Statement = [
      {
        Effect    = "Allow"
        Principal = {
          Service = "ec2.amazonaws.com"
        }
        Action    = "sts:AssumeRole"
      }
    ]
  })
}
```