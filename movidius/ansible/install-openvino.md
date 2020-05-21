# Installing OpenVino toolkit

To install the OpenVino toolkit you should modify **group_vars/movidius.yml** to fit your environment.

> [https://docs.openvinotoolkit.org/latest/_docs_install_guides_installing_openvino_raspbian.html](https://docs.openvinotoolkit.org/latest/_docs_install_guides_installing_openvino_raspbian.html)

This playbook will install the OpenVino on Raspberry pi 3 (Debian Buster).

You will have to have an entry in the **inventory** file for the system where you want to install:

```
$ cat inventory
[raspberry3]
192.168.1.59 ansible_user=pi

[buster]
192.168.1.210 ansible_user=pi

[x86_64]
192.168.1.211 ansible_user=jadebustos

[x240]
192.168.1.211 ansible_user=jadebustos
$
```

```
$ ansible-playbook -i inventory -l buster install-openvino.yml
```

The OpenVino will be downloaded and partially installed.

After that log in the system:

```
$ ssh pi@rsp3b-buster1.lab
Linux rsp3b-buster1.lab 4.19.97-v7+ #1294 SMP Thu Jan 30 13:15:58 GMT 2020 armv7l

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
Last login: Mon May 11 22:17:17 2020 from 192.168.1.42
[setupvars.sh] OpenVINO environment initialized
pi@rsp3b-buster1:~ $ sh /opt/intel/openvino/install_dependencies/install_NCS_udev_rules.sh
Update udev rules so that the toolkit can communicate with your neural compute stick
[install_NCS_udev_rules.sh] udev rules installed
pi@rsp3b-buster1:~ $ 
```

Now you can plug the Intel Movidius Neural Compute Stick.

## Build and Run Object Detection Sample

```
pi@rsp1movidius:~ $ mkdir -p openvino/build
pi@rsp1movidius:~ $ cd openvino/build/
pi@rsp1movidius:~/openvino/build $ cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_CXX_FLAGS="-march=armv7-a" /opt/intel/openvino/deployment_tools/inference_engine/samples
...
-- Build files have been written to: /home/pi/openvino/build
pi@rsp1movidius:~/openvino/build $ make -j2 object_detection_sample_ssd
...
[100%] Built target object_detection_sample_ssd
pi@rsp1movidius:~/openvino/build $ 
```