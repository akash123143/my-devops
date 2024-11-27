
```
Waiting for instances to be ready...
Running Ansible playbook to install Jenkins...

PLAY [Install Jenkins on target machines] ******************************************************************************

TASK [Gathering Facts] *************************************************************************************************
fatal: [MyInstance-1]: UNREACHABLE! => {"changed": false, "msg": "Failed to connect to the host via ssh: remote username contains invalid characters", "unreachable": true}
fatal: [MyInstance-2]: UNREACHABLE! => {"changed": false, "msg": "Failed to connect to the host via ssh: remote username contains invalid characters", "unreachable": true}
fatal: [MyInstance-3]: UNREACHABLE! => {"changed": false, "msg": "Failed to connect to the host via ssh: remote username contains invalid characters", "unreachable": true}

PLAY RECAP *************************************************************************************************************
MyInstance-1               : ok=0    changed=0    unreachable=1    failed=0    skipped=0    rescued=0    ignored=0
MyInstance-2               : ok=0    changed=0    unreachable=1    failed=0    skipped=0    rescued=0    ignored=0
MyInstance-3               : ok=0    changed=0    unreachable=1    failed=0    skipped=0    rescued=0    ignored=0

Error occurred. Exiting...

```



This is the error report today's date is 10-17-2-24
i think this is going to be the final error report 
the problem here is ansible is not able to connect with the created ec2 instances by terraform this is happening because we are using ansible plugin called "aws.ec2 " 

The solution seem to be a proper revision on how this plugin works and updating the details provided in this plugin 

My views are we need to provide the key pair name in the plugin along with configuration files containing the default values 
