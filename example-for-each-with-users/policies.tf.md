### This file defines IAM policies and attaches them to users.

```
resource "aws_iam_policy" "policy" {
  name   = "example_policy"
  policy = <<EOF
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:GetObject"
      ],
      "Resource": "*"
    }
  ]
}
EOF
}

resource "aws_iam_user_policy_attachment" "policy_attachment" {
  for_each = aws_iam_user.iam_users

  user   = each.value.name
  policy_arn = aws_iam_policy.policy.arn
}
```