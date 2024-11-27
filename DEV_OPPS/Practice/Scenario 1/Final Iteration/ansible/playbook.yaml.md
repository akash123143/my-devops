 ```
 ---
- name: Install Git, Python, and pip
  hosts: all
  become: true
  vars:
         ansible_user: ubuntu
         ansible_ssh_private_key_file: /home/web/my_key.pem

  tasks:
    - name: Update apt package index
      apt:
        update_cache: yes

    - name: Install Git
      apt:
        name: git
        state: present

    - name: Install Python
      apt:
        name: python3
        state: present

    - name: Ensure pip is installed
      apt:
        name: python3-pip
        state: present

    - name: Upgrade pip to the latest version
      pip:
        name: pip
        state: latest
```