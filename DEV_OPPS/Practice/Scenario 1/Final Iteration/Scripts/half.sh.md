
```
#!/bin/bash

# Function to handle errors
handle_error() {
    echo "Error occurred. Exiting..."
    exit 1
}

# Terraform commands
echo "Initializing..."
cd /home/web/scene_1/terraform
terraform init || handle_error

echo "please check before making changes..."
terraform plan || handle_error
sleep 60

echo "Applying Terraform configuration to create EC2 instances..."
terraform apply -auto-approve || handle_error

# Wait for instances to be ready
echo "Waiting for instances to be ready..."
sleep 60
echo "your instances are ready to use... you have one hour"

# Wait for a period before cleanup
echo "Standing by before destroying these machines..."
sleep 3600  # Adjust this based on your instance usage

Cleanup (optional)
echo "Destroying Terraform-managed resources..."
terraform destroy -auto-approve || handle_error
```