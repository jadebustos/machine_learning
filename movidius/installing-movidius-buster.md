# Installing Movidius SDK on Debian Buster

Debian Buster is not supported to be installed on Debian Buster (10) but Strech (9).

This is a guide about how to install it in Debian Buster (10).

> As Debian Buster is not supported do not know the problems we can have in the future.

## Manual installation

After cloning the repository:

```
pi@rsp3movidius:~/movidius-sdk $ git clone http://github.com/Movidius/ncsdk
```

+ Copy [install-ncsdk.sh.buster](buster/install-ncsdk.sh.buster) to **/home/pi/movidius-sdk/ncsdk** directory.
+ Replace the **install.sh** script in **/home/pi/movidius-sdk/ncsdk** with [install-buster.sh](buster/install-buster.sh).
+ Perform the installation.