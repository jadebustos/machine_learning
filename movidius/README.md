# Movidius installation

* [Installing Movidius 1 SDK](installing-movidius.md)
* [Installing Movidius 1 SDK in Debian Buster (not Supported)](installing-movidius-buster.md)

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
