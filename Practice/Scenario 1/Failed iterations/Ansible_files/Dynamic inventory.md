save the file as follows to activate the plugin 
aws_ec2.yml

```
plugin: amazon.aws.ec2_instance
regions:
  - ap-south-1
filters:
  instance-state-name: running  # Use the correct filter name
keyed_groups:
  - key: tags.Name
    prefix: instance
hostnames:
  - tag:Name
```

