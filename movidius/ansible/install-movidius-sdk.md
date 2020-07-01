# Installing Movidius 1 SDK

To install the Movidius 1 SDK you should modify **group_vars/movidius.yml** to fit your environment.

This playbook will install the Movidius SDK on Raspberry pi 3 (Debian Buster).

You will have to have an entry in the **inventory** file for the system where you want to install:

```
$ cat inventory
[raspberry3]
192.168.1.59 ansible_user=pi

[rsp1movidius]
192.168.1.210 ansible_user=pi

[x86_64]
192.168.1.211 ansible_user=jadebustos

[x240]
192.168.1.211 ansible_user=jadebustos
$
```

```
$ ansible-playbook -i inventory -l rsp1movidius install-movidius-sdk.yml
```

> Where **rsp1movidius** is the group in the ansible inventory in which you have included your raspberry pi.

The movidius SDK will be downloaded.

After that log in the system:

```
$ cd movidius/movidius-sdk
$ script install.log
Script started, file is install.log
$ make install
....
$ exit
Script done, file is install.log
$
```

and the Movidius SDK will be installed. The installation log wil be stored in **install.log**.

> NOTE: In Debian Stretch (Raspbian) TensorFlow is not supported so it will not be installed.

To install the SDK examples (only in x86_64 it requires TensorFlow to be installed):

```
$ script install-examples.log
$ make examples
./install-opencv.sh

************************ Please confirm *******************************
 Installing OpenCV on Raspberry Pi may take a long time. 
 You may skip this part of the installation in which case some examples 
 may not work without modifications but the rest of the SDK will still 
 be functional. Select n to skip OpenCV installation or y to install it.
 Continue installing OpenCV (y/n) ? n
...
$ exit
Script done, file is install-examples.log
$
```

> Do not install OpenCV, it will be installed with OpenVINO.

## Links

+ [Basic installation and configuration | Intel Movidius Neural Compute Stick SDK Documentation](https://movidius.github.io/ncsdk/install.html).
+ [How to setup the Intel Movidius Neural Compute Stick](https://www.freecodecamp.org/news/how-to-set-up-the-intel-movidius-neural-compute-stick-b9db16d493a7/).
