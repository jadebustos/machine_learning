# x86_64 installation

Install Ubuntu 18.04 Server on a x86_64 computer.

## Prerequisites

+ Enable ssh service and start it:

  ```
  root@raspberrypi:~# systemctl enable ssh
  Synchronizing state of ssh.service with SysV service script with /lib/systemd/systemd-sysv-install.
  Executing: /lib/systemd/systemd-sysv-install enable ssh
  Created symlink /etc/systemd/system/sshd.service → /lib/systemd/system/ssh.service.
  Created symlink /etc/systemd/system/multi-user.target.wants/ssh.service → /lib/systemd/system/ssh.service.
  root@raspberrypi:~# systemctl start ssh
  root@raspberrypi:~# 
  ```

+ Allow your user passwordless sudo:

```
root@ubuntu:~# cat /etc/sudoers.d/jadebustos
jadebustos ALL=(ALL) NOPASSWD: ALL
root@ubuntu:~#
```

+ Copy your ssh key to your user user:

  ```
  [jadebustos@euler ~]$ ssh-copy-id -i .ssh/id_rsa.pub jadebustos@192.168.1.60
  /usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: ".ssh/id_rsa.pub"
  /usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
  /usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
  pi@192.168.1.65's password: 

  Number of key(s) added: 1

  Now try logging into the machine, with:   "ssh 'jadebustos@192.168.1.60'"
  and check to make sure that only the key(s) you wanted were added.
  [jadebustos@euler ~]$
  ```

+ Add the ip to the inventory file in the **[x86_64]** group and the **ansible_user** aswell. Check you can access the computer:

  ```
  [jadebustos@euler ~]$ ansible -i inventory x86_64 -m ping
  192.168.1.60 | SUCCESS => {
      "ansible_facts": {
          "discovered_interpreter_python": "/usr/bin/python"
      },
      "changed": false,
      "ping": "pong"
  }
  [jadebustos@euler ~]$
  ```

+ Modify [group_vars/ubuntu.yml](group_vars/ubuntu.yml), [group_vars/x86_64.yml](group_vars/x86_64.yml) and [group_vars/network.yml](group_vars/network.yml) to fit you environment.

    ```
    $ ansible-playbook -i inventory -l x86_64 configure-os-x86_64.yml
    ```

The computer will be rebooted.

After that your computer will have a static ip configured and you should add the following to the **inventory** file:

```
[x86_64]
192.168.1.211 ansible_user=jadebustos
```



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