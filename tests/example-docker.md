### Example docker container to run the all the test

```dockerfile
# Use an official Go runtime as a parent image
FROM golang:latest

# Set the working directory in the container
WORKDIR /app

# Install Terraform
RUN wget https://releases.hashicorp.com/terraform/1.0.8/terraform_1.0.8_linux_amd64.zip && \
    unzip terraform_1.0.8_linux_amd64.zip && \
    mv terraform /usr/local/bin/ && \
    rm terraform_1.0.8_linux_amd64.zip

# Install TFLint
RUN wget https://github.com/terraform-linters/tflint/releases/latest/download/tflint_linux_amd64.zip && \
    unzip tflint_linux_amd64.zip && \
    mv tflint /usr/local/bin/ && \
    rm tflint_linux_amd64.zip

# Install other necessary tools (e.g., wget, unzip)
RUN apt-get update && \
    apt-get install -y wget unzip

# Copy the script files into the container
COPY static_analysis.sh /app
COPY unit_test.go /app
COPY integration_test.go /app
COPY lint.sh /app

# Make the scripts executable
RUN chmod +x static_analysis.sh unit_test.go integration_test.go lint.sh

# Run the static analysis script by default when the container starts
CMD ["./static_analysis.sh"]
```

In this Dockerfile:

1. We start from the official Go image to have the Go runtime installed.
2. We install Terraform and TFLint.
3. We copy the script files (`static_analysis.sh`, `unit_test.go`, `integration_test.go`, `lint.sh`) into the container.
4. We make the scripts executable.
5. We set `static_analysis.sh` as the default command to run when the container starts.