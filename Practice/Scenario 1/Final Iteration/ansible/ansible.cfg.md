
```
[defaults]
inventory = ./aws_ec2.yaml  # Path to your inventory file
remote_user = ubuntu        # Change if using a different AMI (e.g., ubuntu for Ubuntu)
private_key_file = /home/web/my_key.pem  # Update with your actual path to the private key
host_key_checking = False   # Disable host key checking for new hosts
```