# preseed-testing

Runs a custom preseed file against a VirtualBox VM in order to test an automated installation of an Ubuntu 18.04 server

* Downloads ubuntu netinstall for Ubuntu 18.04
* Builds a custom install ISO
* Creates a VirtualBox VM
* Loads a custom preseed file called "custom.cfg"
* Runs the preseed file against the VM

## Requirements

Linux system with Virtualbox for install testing.

```shell
/usr/bin/vboxmanage
/usr/bin/xorriso
/usr/bin/7z
/usr/bin/sha1sum
```

## nvme drives

For nvme drive you will want to execute **build-and-run-dual-nvme-drives**

For other drives use **build-and-run**

## Encrypted User Passwords

This does not show the password on the process list. For more options see openssl passwd

```shell
openssl passwd -1 -stdin <<< password_here
```

## Getting started

Run `build-and-run` which will download some extra dependencies, build image and start
a Virtualbox machine to test the install process.

## Putting the image into usb stick

Assuming usb stick is `/dev/sdc` and the pre-built image name is install.iso:

```
sudo dd bs=1M if=install.iso of=/dev/sdc
```

## Ubuntu LTS installer documentation

install methods:

1. Ubiquity installer (which is a fairly limited install from a pre-built complete system 
   image).
2. Network install using [Debian Installer][1].

This customized installer is the "Debian installer" flavour. Best place for documentation
is Debian docs.

[1]: https://wiki.debian.org/DebianInstaller/

## Reference

* Cloned from https://github.com/tadas-s/custom-ubuntu-install then modified

