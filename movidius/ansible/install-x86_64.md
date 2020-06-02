# x86_64 installation

Install Ubuntu 16.04 Desktop on a x86_64 computer.

## Configuration and deployment 

+ Modify **inventory** to configure your DHCP assigned IP in **x86_64**.

   ```
   $ cat inventory
   [raspberry3]
   192.168.1.59 ansible_user=pi

   [x86_64]
   192.168.1.61 ansible_user=jadebustos
   $
   ```

+ Set the **ansible_user** to the user you copied you ssh public key.

+ You will need to create a file in **/etc/sudoers.d** with the following:

  ```
  jadebustos ALL=(ALL) NOPASSWD: ALL
  ```

> Replace **jadebustos** with your username (the one where you copy the ssh public key). This will allow you user to assume root role without asking password. It is required for ansible to perform privileges actions.

+ Modify **group_vars/debian.yml** and **group_vars/network.yml** to fit you environment.

   You can check that ansible can access your computer:

   ```
   $ ansible -i inventory x86_64 -m ping
   192.168.1.61 | SUCCESS => {
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
$ ansible-playbook -i inventory -l x86_64 configure-os-x86_64.yml
```

The computer will be rebooted after installation.

After that your computer will have a static ip configured and you should add the following to the **inventory** file:

```
[x240]
192.168.1.211 ansible_user=jadebustos
```

> **x240** is the name you configured in **group_vars/x86_64.yml** and the ip is the ip you configured in the above file. **jadebustos** is your username in the x86_64 computer.

## Install Intel Movidius SDK

[Install Intel Movidius SDK](install-movidius-sdk.md)