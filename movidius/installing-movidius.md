# Installing Movidius 1 SDK

## Supported Operating Systems

The following are the supported Operating Systems:

+ [Ubuntu 16.04 for x86_64](ansible/install_x86_64.md)
+ [Debian Stretch for Raspberry Pi](ansible/install_raspberry.md)


## Build and run examples

You need to install [OpenVINO toolkit](installing-openvino.md) before continuing.

Clone the example repository and build the examples:

```
pi@rsp3movidius:~/movidius $ git clone https://github.com/movidius/ncappzoo.git
pi@rsp3movidius:~/movidius $ cd ncappzoo
pi@rsp3movidius:~/movidius $ make 
```

