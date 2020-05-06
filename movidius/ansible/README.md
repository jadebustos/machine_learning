# Ansible playbooks to automate installation

These playbooks have been developed to ease **Intel Movidius Nerual Compute Stick** on:

+ **Rasberry Pi 3** running **Raspbian (Debian Stretch)**.
+ **x86_64** computer running **Ubuntu 16.04**.

## Requirements

+ Configure Wifi.
+ Enable ssh service.
+ Copy your public key to the **pi** user on **raspberry** and to your user on a **x86_64** computer.

```
$ ssh-copy-id -i ~/.ssh/id_rsa.pub pi@hostname
```

## Installation

+ [Raspberry pi 3 installation](install-raspberry.md)
+ [x86_64 computer installation](install-x86_64.md)