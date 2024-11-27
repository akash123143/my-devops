
The functionality of this  configuration file is, it creates a aws security group called "sec-group2" that allows communication over port 22 for ssh traffic  and then creates 3 ec2 instances , all these are done in ap-south-1 availability zone (Mumbai)




```
provider "aws" {
  region = "ap-south-1"  # Change to your preferred region
}

resource "aws_security_group" "sec_group2" {
  name        = "sec-group2"
  description = "Security group for SSH access"

  ingress {
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]  # Adjust this to restrict access to specific IPs if needed
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"  # Allow all outbound traffic
    cidr_blocks = ["0.0.0.0/0"]
  }
}

resource "aws_instance" "my_instances" {
  count         = 3
  ami           = "ami-02a92eb3016dca139"  # this is ubuntu with required architecture ami
  instance_type = "t2.micro"

  vpc_security_group_ids = [aws_security_group.sec_group2.id]  # Attach the new security group

  user_data = <<-EOF
              #!/bin/bash
              mkdir /home/ubuntu/.ssh
              chmod 700 /home/ubuntu/.ssh
              echo "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQC9a0E1iYk7NkQIMy+Qd7TrJfOZDu/IHfJ2MqtL8D/GvY4LZlXyjmBMChT/ng3YWTDBCPcSNwf2RiL4DQv28C01dL5LCum7x5QwAm3qlV1YUOORRdCaNYKBMi/ApEcuzSt+xdiN3aJ8JUfPjfBHPHFT1Q7eHXUUHSxvvroVVEdSHuDKajS0tU0uaBx+jc+VqQgidtP4ER1SL4Mjd1XAMq02jW9j5dv6IpJy0YE7CJJYvdBwC1FuKdACWpstvh7XR5iFz8u/1IUcn1YJMbsB+VT20fCRFLd6fhamPYCp3mlY6mRUxlbhh08D878Z2gW4nBUqna31gmt4+TPkg0FphpdplGdH4ZY3BlTYjT0S2FSn12FRmK+DYkkC1WhtiUhYUW/nfjQOU0OgIIq/cIS/TTbxeeegR/wYS0xVY9WXFcdmryHDIxUG/e/zzZ57FF/mrmlQtnqyCMxAR2YqZWiEdG5F83fXXBVewCbXYH8gOUKlTegZZMvJuxjLXsOnsEKyPv9lMIGsYDYlOMLfGf6HzOyFTWrfsE45c+wlocrt9bJDebLSWyiG3foaUO8uUV4HU6PJRTK4z2iKL06bk+OAKGq7fuLUrIyOAKGkDD3+Dv5m6Nx/+doPutOHti2sjEQXYaz2HPlnALBbDD8zE8jurGG8CJ33xdKIYAex47SyCPmKGQ== akash.kondamudi1@gmail.com" >> /home/ubuntu/.ssh/authorized_keys
              chmod 600 /home/ubuntu/.ssh/authorized_keys
              chown ubuntu:ubuntu /home/ubuntu/.ssh/authorized_keys
              EOF

  tags = {
    Name = "MyInstance-${count.index + 1}"
  }
}

output "instance_ips" {
  value = aws_instance.my_instances[*].public_ip
}

```