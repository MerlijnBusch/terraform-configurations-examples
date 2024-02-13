### Here's an example of how you can create a custom IAM policy in Terraform to grant access to a specific Amazon RDS database:

```
data "aws_region" "current" {}

data "aws_rds_cluster" "example" {
  cluster_identifier = "your-rds-cluster-identifier"
  region            = data.aws_region.current.name
}

resource "aws_iam_policy" "rds_access_policy" {
  name        = "rds-access-policy"
  path        = "/"
  description = "Allows access to a specific RDS database"

  policy = jsonencode({
    Version = "2012-10-17",
    Statement = [
      {
        Effect   = "Allow",
        Action   = [
          "rds-data:ExecuteStatement",
          "rds-data:BatchExecuteStatement",
          "rds:DescribeDBClusters",
          "rds:DescribeDBInstances",
          "rds:DescribeDBClusterEndpoints",
          "rds:DescribeDBClusterSnapshots",
          "rds:DescribeDBClusterBacktracks",
          "rds:DescribeDBClusterEndpoints",
          "rds:DescribeDBClusterParameterGroups",
          "rds:DescribeDBClusterParameters",
          "rds:DescribeDBClusterSnapshotAttributes",
          "rds:DescribeDBClusterSnapshots",
          "rds:DescribeDBEngineVersions",
          "rds:DescribeDBLogFiles",
          "rds:DescribeDBParameters",
          "rds:DescribeDBSecurityGroups",
          "rds:DescribeDBSubnetGroups",
          "rds:DescribeEventCategories",
          "rds:DescribeEvents",
          "rds:DescribeOrderableDBInstanceOptions",
          "rds:ListTagsForResource",
          "rds:ViewEngineDefaultClusterParameters",
          "rds:ViewDBCluster",
          "rds:ViewDBClusterEndpoints"
        ],
        Resource = [
          aws_rds_cluster.example.arn
          # Add other resources as needed, such as specific databases within the cluster
        ]
      }
    ]
  })
}

resource "aws_iam_policy_attachment" "rds_access_attachment" {
  name       = "rds-access-attachment"
  users      = [aws_iam_user.example.name]
  policy_arn = aws_iam_policy.rds_access_policy.arn
}
```

**In this example:**

1. **Fetch RDS Cluster Details**: We first fetch the details of the RDS cluster using `aws_rds_cluster`.

2. **Define IAM Policy**: We then define an IAM policy (`aws_iam_policy`) that grants permissions to interact with the RDS cluster and its resources. Adjust the actions and resources as needed to match your requirements.

3. **Attach IAM Policy**: Finally, we attach this IAM policy to the user (`aws_iam_policy_attachment`) to grant them access to the specified RDS database.
