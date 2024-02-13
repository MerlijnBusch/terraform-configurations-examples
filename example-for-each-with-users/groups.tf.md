### groups.tf: This file defines IAM groups and assigns users to them.

```
resource "aws_iam_group" "group" {
  name = "example_group"
}

resource "aws_iam_group_membership" "group_membership" {
  for_each = aws_iam_user.iam_users

  name    = each.key
  users   = [each.value.name]
  group   = aws_iam_group.group.name
}
```