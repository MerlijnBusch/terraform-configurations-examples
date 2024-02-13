### Here's an example `main.tf` file with configurations for two different providers: AWS and Google Cloud Platform (GCP).

```
# Configure AWS Provider
provider "aws" {
  region     = "us-west-2"
  access_key = "your-aws-access-key"
  secret_key = "your-aws-secret-key"
}

# Configure GCP Provider
provider "google" {
  credentials = file("path/to/gcp_credentials.json")
  project     = "your-gcp-project-id"
  region      = "us-central1"
}
```

In this example:

1. We're configuring the AWS provider with the region set to `us-west-2` and providing access and secret keys for authentication.
2. For the GCP provider, we're providing the path to a service account key file (`gcp_credentials.json`), specifying the GCP project ID, and setting the region to `us-central1`.