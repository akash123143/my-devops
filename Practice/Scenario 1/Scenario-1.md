lets write a shell  script that automates all these steps when its run 

1. Install terraform 
2. create two ec2 instances in a zone
3. add this zone to ansible 
4. install jenkins in the machines of this zone.

In this practice scenario i am going to create two ec2 instance through the Terraform and add this  two instances ec2 in ansible and install jenkins in this machines through ansible. 


==**Terraform configuration file**== [[main.tf]] : This code automatically creates 3 ec2 instances when the terraform command are followed and automatically adds my  machines ssh public key to these machines, once the creation is done it returns the public IP addresses of these machines.

==**Ansible inventory file**== [[aws_ec2.yaml]] : this code automatically fetches all the running ec2 instances form the availability zone set in the terraform configuration file.

 ==**Ansible playbook**== [[playbook.yaml]] : Primarily this playbook is intended to install jenkins in all the instances but at the end we changed it to a simple task because of the lack of knowledge of the functions of Jenkins, once after completion of the jenkins chapter we can try this again with jenkins.


[[Extras]] : this file is used to store the data of all the failed iterations for revision purpose.
