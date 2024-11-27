
playbook.yml



```
---
- name: Install Jenkins on target machines
  hosts: all
  become: true
  tasks:
    - name: Install Java (required for Jenkins)
      apt:
        name: openjdk-11-jdk
        state: present
        update_cache: yes

    - name: Add Jenkins repository key
      apt_key:
        url: https://pkg.jenkins.io/keys/jenkins.io.key
        state: present

    - name: Add Jenkins repository
      apt_repository:
        repo: deb http://pkg.jenkins.io/debian/ stable main
        state: present

    - name: Install Jenkins
      apt:
        name: jenkins
        state: present
        update_cache: yes

    - name: Start Jenkins service
      systemd:
        name: jenkins
        state: started
        enabled: yes

    - name: Open Jenkins port (8080)
      ufw:
        rule: allow
        name: 'Jenkins'
        port: 8080
        proto: tcp
```