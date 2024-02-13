### This file defines the users and creates IAM users for each user.

```
variable "users" {
  type    = list(string)
  default = ["user1", "user2", "user3"]
}

resource "aws_iam_user" "iam_users" {
  for_each = { for user in var.users : user => user }

  name = each.key
}
```