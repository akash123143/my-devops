
```
plugin: aws_ec2
regions:
  - ap-south-1
filters:
  instance-state-name: running
keyed_groups:
  - key: tags
```