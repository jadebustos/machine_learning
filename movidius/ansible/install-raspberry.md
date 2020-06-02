# Raspberry installation

Install raspbian (Debian Stretch) on your raspberry pi 3.

## Configuration and deployment 

+ Modify **inventory** to configure your raspberry DHCP assigned IP in **raspberry3**.

   ```
   $ cat inventory
   [raspberry3]
   192.168.1.59 ansible_user=pi
   $
   ```

+ Modify **group_vars/raspberry.yml**, **group_vars/debian.yml** and **group_vars/network.yml** to fit you environment.

   You can check that ansible can access your computer:

   ```
   $ ansible -i inventory raspberry3 -m ping
   192.168.1.59 | SUCCESS => {
       "ansible_facts": {
           "discovered_interpreter_python": "/usr/bin/python"
       },
       "changed": false,
       "ping": "pong"
   }
   $
   ```

Execute:

```
$ ansible-playbook -i inventory -l raspberry3 configure-os-raspberry.yml
```

The raspberry pi will be rebooted.

After that your raspberry pi has a static ip configured and you should add the following to the **inventory** file:

```
[rsp3movidius]
192.168.1.213 ansible_user=pi
```

> **rsp3movidius** is the name you configured in **group_vars/raspberry.yml** and the ip is the ip you configured in the above file.

## Install Intel Movidius SDK

[Install Intel Movidius SDK](install-movidius-sdk.md)