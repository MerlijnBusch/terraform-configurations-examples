
### This file will contain the definition of the IAM group and its attachments.

```
# IAM Group Definition
resource "aws_iam_group" "example_group" {
  name = "example-group"
}

# IAM Group Membership
resource "aws_iam_group_membership" "example_group_membership" {
  name  = "example-group-membership"
  users = ["example-user"]
  group = aws_iam_group.example_group.name
}

# IAM Role Attachments to Group
resource "aws_iam_group_policy_attachment" "example_group_policy_attachment_1" {
  group      = aws_iam_group.example_group.name
  policy_arn = aws_iam_role.example_role_1.arn
}

resource "aws_iam_group_policy_attachment" "example_group_policy_attachment_2" {
  group      = aws_iam_group.example_group.name
  policy_arn = aws_iam_role.example_role_2.arn
}
```

### IAM Roles Configuration:

* **IAM Role Definitions**:
    * Two IAM roles are defined in this section: `example_role_1` and `example_role_2`.
    * Each role has a unique name and an associated trust relationship policy allowing the EC2 service to assume the role.

### Group Configuration:

* **IAM Group Definition**:
    * An IAM group named `example-group` is defined in this section.
    * This group will be used to organize users and manage their permissions.

* **IAM Group Membership**:
    * A user named `example-user` is added to the IAM group.
    * This ensures that the user inherits the permissions assigned to the group.

* **IAM Role Attachments to Group**:
    * Both IAM roles (`example_role_1` and `example_role_2`) are attached to the IAM group.
    * This means that any user belonging to the group will inherit the permissions associated with these roles.
