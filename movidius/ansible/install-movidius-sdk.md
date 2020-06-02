# Installing Movidius 1 SDK

To install the Movidius 1 SDK you should modify **group_vars/movidius.yml** to fit your environment.

This playbook will install the Movidius SDK on Raspberry pi 3 (Debian Stretch) or in a x86_64 computer (Ubuntu 16.04).

You will have to have an entry in the **inventory** file for the system where you want to install:

```
$ cat inventory
[raspberry3]
192.168.1.59 ansible_user=pi

[rspmovidius1]
192.168.1.210 ansible_user=pi

[x86_64]
192.168.1.211 ansible_user=jadebustos

[x240]
192.168.1.211 ansible_user=jadebustos
$
```

```
$ ansible-playbook -i inventory -l movidius1 install-movidius-sdk.yml
```

> Where **movidius1** is the group in the ansible inventory in which you have included your raspberry pi.

The movidius SDK will be downloaded.

After that log in the system:

```
$ cd movidius/movidius-sdk
$ script install.log
Script started, file is install.log
$ make install
....
$ exit
$
```

and the Movidius SDK will be installed. The installation log wil be stored in **install.log**.

> NOTE: In Debian Stretch TensorFlow is not supported so it will not be installed.

## Links

+ [Basic installation and configuration | Intel Movidius Neural Compute Stick SDK Documentation](https://movidius.github.io/ncsdk/install.html)
