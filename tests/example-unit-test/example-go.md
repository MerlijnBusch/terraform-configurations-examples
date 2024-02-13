### example of how you could write a unit test script using Terratest, a popular Go library for testing infrastructure code, to validate individual Terraform modules:

```go
// filename: unit_test.go

package test

import (
    "testing"
    "github.com/stretchr/testify/assert"
    "github.com/gruntwork-io/terratest/modules/terraform"
)

func TestTerraformModule(t *testing.T) {
    // Path to the Terraform directory containing the module to test
    terraformOptions := &terraform.Options{
        TerraformDir: "path/to/your/terraform/module",
    }

    // Run `terraform init` and `terraform apply` to deploy the Terraform module
    terraform.InitAndApply(t, terraformOptions)

    // Run tests to validate the behavior of the module
    output := terraform.Output(t, terraformOptions, "example_output")
    assert.Equal(t, "expected_value", output)

    // Clean up resources by running `terraform destroy`
    defer terraform.Destroy(t, terraformOptions)
}
```

This test script uses Terratest to:

1. Deploy the Terraform module located at the specified directory.
2. Retrieve the output of the deployed resources using `terraform.Output`.
3. Assert that the output matches the expected value using `assert.Equal`.
4. Clean up resources by running `terraform.Destroy` after the tests are completed.

To run this test, make sure you have Go installed and then run:

```shell
go test -v unit_test.go
```
