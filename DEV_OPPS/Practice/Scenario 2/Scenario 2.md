
In this simulation we we will create a security group with ssh access and create three ec2 instances in this security group and then use Ansible to configure those machines. The difference between the previous scenario and this scenario is in the previous version we use ansible dynamic inventory with aws.ec2 plugin to fetch all the instances in an availability zone and configure them, this time we use the output from the terraform (public IP addresses of the created machines) to append into a .yaml file to later use this as Ansible inventory file .



