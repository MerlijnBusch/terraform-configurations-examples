
### This file will contain the definitions of IAM roles.

```
# IAM Role Definitions
resource "aws_iam_role" "example_role_1" {
  name               = "example-role-1"
  assume_role_policy = jsonencode({
    "Version": "2012-10-17",
    "Statement": [{
      "Effect": "Allow",
      "Principal": { "Service": "ec2.amazonaws.com" },
      "Action": "sts:AssumeRole"
    }]
  })
}

resource "aws_iam_role" "example_role_2" {
  name               = "example-role-2"
  assume_role_policy = jsonencode({
    "Version": "2012-10-17",
    "Statement": [{
      "Effect": "Allow",
      "Principal": { "Service": "ec2.amazonaws.com" },
      "Action": "sts:AssumeRole"
    }]
  })
}
```

### IAM Roles Configuration:

* **IAM Role Definitions**:
    * Two IAM roles are defined in this section: `example_role_1` and `example_role_2`.
    * Each role has a unique name and an associated trust relationship policy allowing the EC2 service to assume the role.
