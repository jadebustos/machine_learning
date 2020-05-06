# Installing Movidius 1 SDK

## Supported Operating Systems

The following are the supported Operating Systems:

+ Ubuntu 16.04 for x86_64.
+ Debian Stretch for Raspberry Pi.

## SDK Installation

Clone the SDK repository:

```
pi@rsp3movidius:~/movidius-sdk $ git clone http://github.com/Movidius/ncsdk
```

So the SDK will be at **/home/pi/movidius-sdk/ncsdk**.

To install it:

```
pi@rsp3movidius:~/movidius-sdk $ cd ncsdk
pi@rsp3movidius:~/movidius-sdk/ncsdk $ script movidius-installation.log
Script started, file is movidius-installation.log
pi@rsp3movidius:~/movidius-sdk/ncsdk $ make install
...
pi@rsp3movidius:~/movidius-sdk/ncsdk $ exit
exit
Script done, file is movidius-installation.log
pi@rsp3movidius:~/movidius-sdk/ncsdk $
```

> File **movidius-installation.log** will store the log installation.