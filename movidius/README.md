# Movidius installation

* [Installing Movidius 1 on x86_64](ansible/install-x86_64.md)
* [Installing Movidius 1 on Raspbian (Stretch)](ansible/install-raspberry.md)

## Requirements

+ Configure Wifi.
+ You need to install the **ssh** server:

  ```
  # apt install openssh-server
  ...
  # systemctl enable ssh
  # systemctl start ssh
  #
  ```
+ Copy your public key to the **pi** user on **raspberry** and to your user on a **x86_64** computer.

  ```
  $ ssh-copy-id -i ~/.ssh/id_rsa.pub pi@hostname
  ```
