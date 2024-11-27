
```
[defaults]
inventory = ./aws_ec2.yml  # Path to your inventory file
remote_user = ubuntu  # Change if using a different AMI (e.g., ubuntu for Ubuntu)
private_key_file = ~/.ssh/id_rsa # Path to your private key
host_key_checking = False  # Optional: Disable host key checking for new hosts
```