# Raspberry installation

Install raspbian (Debian Buster) on your Raspberry pi 3.

## Prerequisites

+ After installation configure wifi connection on the Raspberry.

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

+ Copy your ssh key to **pi** user:

  ```
  [jadebustos@euler ~]$ ssh-copy-id -i .ssh/id_rsa.pub pi@192.168.1.65
  /usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: ".ssh/id_rsa.pub"
  /usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
  /usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
  pi@192.168.1.65's password: 

  Number of key(s) added: 1

  Now try logging into the machine, with:   "ssh 'pi@192.168.1.65'"
  and check to make sure that only the key(s) you wanted were added.
  [jadebustos@euler ~]$
  ```

+ Add the ip to the inventory file in the **[raspberry3]** group. Check you can access the raspberry pi:

  ```
  [jadebustos@euler ~]$ ansible -i inventory raspberry3 -m ping
  192.168.1.65 | SUCCESS => {
      "ansible_facts": {
          "discovered_interpreter_python": "/usr/bin/python"
      },
      "changed": false,
      "ping": "pong"
  }
  [jadebustos@euler ~]$
  ```

+ Modify [group_vars/raspberry.yml](group_vars/raspberry.yml), [group_vars/debian.yml](group_vars/debian.yml) and [group_vars/network.yml](group_vars/network.yml) to fit you environment.

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

To install the Movidius 1 SDK you should modify **group_vars/movidius.yml** to fit your environment. Maybe you want to change these variables to use newer versions:

+ **openvino_toolkit** 
+ **openvino_toolkit_filename**
+ **pretrained_face_model**
+ **pretrained_topology**

You can follow the official guide to install [OpenVINO toolkit in Raspbian](https://docs.openvinotoolkit.org/latest/_docs_install_guides_installing_openvino_raspbian.html) or you can install it using this ansible playbook:

```
[jadebustos@euler ~]$ ansible-playbook -i inventory -l rsp3movidius install-openvino.yml
...
[jadebustos@euler ~]$
```

Now it is time to plug the NCS. Log into the Raspberry pi to be certain that OpenVINO environment is loaded and then:

```
pi@rsp3movidius:~ $ source /opt/intel/openvino/install_dependencies/install_NCS_udev_rules.sh 
Updating udev rules...
Udev rules have been successfully installed.
pi@rsp3movidius:~ $ cd /opt/intel/openvino/build/
pi@rsp3movidius:/opt/intel/openvino/build $ 
```
