[[Ansible Terminology]]

Ansible is a configuration management tool using which we can manage and maintain settings, maintenance necessary applications, files in a small/large number of machines all at once instead of doing it one machine at a time.

Ansible need a key-less authentication to operate, on its slave devices.

Ansible have two major files 
	1. Inventory file
	2. Playbook file 

Both these file are written in .Yaml format. 
#### Inventory file :
	The inventory file keeps the list of file servers (slaves systems) to be controled by the master machine (The machine in which Ansible is installed and running).

#### Playbook file :
	Ansible playbook contains the instructions on whath actions are to be taken by the Ansible in its slave machines, like what applications are to be present, what settings are to be adjusted, what services are to be up and running etc

==Ansible can also be used to create and destroy machines in a cloud provider using ansible plugins just like a infrastructure management tool, but it is not as effective as a native infrastructure management tool like Terraform.==


#### ==Example Inventory file


```
all:
  hosts:
    webserver1:
      ansible_host: 192.168.1.10
      ansible_user: admin
      role: web
    webserver2:
      ansible_host: 192.168.1.11
      ansible_user: admin
      role: web
    dbserver:
      ansible_host: 192.168.1.20
      ansible_user: admin
      role: database
  children:
    webservers:
      hosts:
        webserver1:
        webserver2:
    databases:
      hosts:
        dbserver:

```

#### ==Example playbook file 

```
---
- name: Install Nginx on web servers
  hosts: webservers
  become: yes
  tasks:
    - name: Update apt package cache
      apt:
        update_cache: yes

    - name: Install Nginx
      apt:
        name: nginx
        state: present

    - name: Start Nginx service
      service:
        name: nginx
        state: started
        enabled: yes

    - name: Create a custom index.html
      copy:
        content: "<h1>Welcome to Nginx!</h1>"
        dest: /var/www/html/index.html

```

### Dynamic Inventory

Ansible contains a feature called Dynamic inventory, which implies the the number of servers may scale up and scale down dynamically and Ansible automatically detects and performs its actions in all the newly added machines. A dynamic inventory file is usually written in python are any other scripting language the output format must be in .json format, it can be configured by specifying the script file in  ===Ansible.cfg=== file, these scripts usually are built in scripts of for each cloud provided these scripts are further modified with adding credentials and using filters, like location of data center based or VPC. 

#### ==Example Dynamic Inventory file

```
# Minimal example using environment vars or instance role credentials
# Fetch all hosts in us-east-1, the hostname is the public DNS if it exists, otherwise the private IP address

plugin: amazon.aws.aws_ec2
regions:
  - us-east-1

---
```

#### [[Ansible collection]]

#### [[Ansible roles]]




