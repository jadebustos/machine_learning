# Installing Movidius 1 SDK

## Supported Operating Systems

The following are the supported Operating Systems:

+ Ubuntu 16.04 for x86_64.
+ Debian Stretch for Raspberry Pi.

## SDK Installation

Clone the SDK repository:

```
pi@rsp3movidius:~/movidius/movidius-sdk $ git clone http://github.com/Movidius/ncsdk
```

So the SDK will be at **/home/pi/movidius/movidius-sdk/ncsdk**.

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

> If you want to install it in a python virtualenv add **USE_VIRTUALENV=yes** to **ncsdk.conf** file.

## Build and run examples

You need to install [OpenVINO toolkit](installing-openvino.md) before continuing.

Clone the example repository and build the examples:

```
pi@rsp3movidius:~/movidius $ git clone https://github.com/movidius/ncappzoo.git
pi@rsp3movidius:~/movidius $ cd ncappzoo
pi@rsp3movidius:~/movidius $ make 
```

