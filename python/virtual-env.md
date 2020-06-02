# How to create a python virtual environment

In Ubuntu you need to install:

```
# apt install build-essential libssl-dev libffi-dev python-dev python3-pip 
# pip install virtualenv
```

Create the python 3 virtual environment:

```
$ virtualenv -p python3 my-virtual-environment
```

You can create the virtual environment with any user. This will create the directory **my-virtual-environment** where the virtual environment will be created.

To use it:

```
$ ls -lh
drwxr-xr-x. 2 root root   55 May  7 02:12 my-virtual-environment
$ . my-virtual-environment/bin/activate
(my-virtual-environment) $
```

So you can use your virtual environment, install your python modules using pip, ...

To finish to use:

```
(my-virtual-environment) $ deactivate
$
```
