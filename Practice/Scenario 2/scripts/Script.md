
This script uses terraform to build machines in aws and fetches the IP addresses of the machines to create ansible inventory file, it also installs the necessary programs to perform the task and further uses ansible to configure those machines using a playbook. 

```
#!/bin/bash

# Function to handle errors
handle_error() {
    echo "Error occurred: $1. Exiting..."
    exit 1
}

# Function to install jq if not present
install_jq() {
    echo "Installing jq..."
    if command -v apt-get &> /dev/null; then
        sudo apt-get update && sudo apt-get install -y jq || handle_error "Failed to install jq"
    elif command -v yum &> /dev/null; then
        sudo yum install -y jq || handle_error "Failed to install jq"
    else
        handle_error "Unsupported package manager. Please install jq manually."
    fi
}

# Function to check command availability
check_command() {
    command -v "$1" &> /dev/null || handle_error "$1 command not found. Please install it."
}

# Check for required commands
check_command "terraform"
check_command "ansible-playbook"
check_command "jq"

# Define paths
TERRAFORM_DIR="/home/web/scene_1/terraform"
ANSIBLE_DIR="/home/web/scene_1/ansible"
ANSIBLE_INVENTORY_FILE="$ANSIBLE_DIR/aws_ec2.yaml"

# Check if jq is installed
if ! command -v jq &> /dev/null; then
    install_jq
fi

# Terraform commands
echo "Initializing Terraform..."
cd "$TERRAFORM_DIR" || handle_error "Failed to change directory to $TERRAFORM_DIR"
terraform init || handle_error "Terraform init failed"

echo "Please check before making changes..."
terraform plan || handle_error "Terraform plan failed"
sleep 60  # Consider replacing with a readiness check

echo "Applying Terraform configuration to create EC2 instances..."
terraform apply -auto-approve || handle_error "Terraform apply failed"

# Wait for instances to be ready
echo "Waiting for instances to be ready..."
sleep 50  # Adjust this based on your instance startup time

# Fetch public IP addresses from Terraform output
echo "Fetching public IP addresses from Terraform output..."
IP_ADDRESSES=$(terraform output -json instance_ips | jq -r '.[]')

# Clear the Ansible inventory file before appending new IP addresses
> "$ANSIBLE_INVENTORY_FILE"
echo "Updating Ansible inventory file with the following IP addresses:"
for ip in $IP_ADDRESSES; do
    echo "- $ip" >> "$ANSIBLE_INVENTORY_FILE"
    echo "$ip"
done

# Ansible commands
echo "Running Ansible playbook to install Jenkins..."
cd "$ANSIBLE_DIR" || handle_error "Failed to change directory to $ANSIBLE_DIR"
ansible-playbook -i aws_ec2.yaml playbook.yaml || handle_error "Ansible playbook execution failed"

# Wait for a period before cleanup
echo "Standing by before destroying these machines..."
sleep 1800  # Adjust this based on your instance usage

# Cleanup
echo "Destroying Terraform-managed resources..."
terraform destroy -auto-approve || handle_error "Terraform destroy failed"
```

