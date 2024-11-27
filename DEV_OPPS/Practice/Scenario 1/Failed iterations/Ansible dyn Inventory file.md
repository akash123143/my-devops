We are using a aws.ec2 ansible plugin for the dynamic inventory file to fetch all the running ec2 instances from an availability zone. this file is always saved in **.yaml** formant. The code will be as follows. 

```
plugin: aws_ec2
regions:
  - us-west-2  # Replace with your desired AWS region
filters:
  instance-state-name: running  # Optional: include only running instances
keyed_groups:
  - key: tags
    prefix: tag
hostnames:
  - tag:Name  # Use the Name tag for the hostname
compose:
  ansible_host: public_ip_address  # Use public IP address as the ansible_host

```

