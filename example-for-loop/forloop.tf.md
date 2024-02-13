
### This file we create an example for loop

```
# Define a list of instance types and their corresponding tags
variable "instance_types" {
  default = [
    { type = "t2.micro", tag = "micro" },
    { type = "t2.small", tag = "small" },
    { type = "t2.medium", tag = "medium" }
  ]
}

# Create EC2 instances with different instance types and tags
resource "aws_instance" "example_instances" {
  count         = length(var.instance_types)  # Loop over the instance_types list
  ami           = "ami-0c55b159cbfafe1f0"  # Example AMI ID (Amazon Linux 2)
  instance_type = var.instance_types[count.index].type  # Set the instance type from the list
  tags = {
    Name = "example-instance-${var.instance_types[count.index].tag}"  # Dynamically set the instance name using the tag
  }
}
```

### Configuration Explanation:

* **Defining a list of instance types and their corresponding tags**:
    * The `variable` block defines a variable named `instance_types`, which is a list of objects.
    * Each object in the list has two attributes: `type` (representing the instance type) and `tag` (representing a tag associated with that instance type).

* **Creating EC2 instances with different instance types and tags**:
    * The `resource` block defines an AWS EC2 instance resource named `example_instances`.
    * This block uses the `count` meta-argument to iterate over the `instance_types` list.
    * `count = length(var.instance_types)`: Specifies the number of instances to create, which is equal to the length of the `instance_types` list.
    * `ami = "ami-0c55b159cbfafe1f0"`: Specifies the Amazon Machine Image (AMI) ID to use for the instances.
    * `instance_type = var.instance_types[count.index].type`: Sets the instance type for each instance.
    * `tags = { ... }`: Specifies the tags to assign to each instance. The `Name` tag is set dynamically using interpolation to include the tag associated with the current instance type.
