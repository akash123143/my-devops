

```
#!/bin/bash

# Function to handle errors
handle_error() {
    echo "Error occurred. Exiting..."
    exit 1
}


# Ansible commands
echo "Running Ansible playbook to install Jenkins..."
cd /home/web/scene_1/ansible
ansible-playbook -i aws_ec2.yaml playbook.yaml || handle_error

# Wait for a period before cleanup
echo "Standing by before destroying these machines..."
sleep 1800  # Adjust this based on your instance usage
```