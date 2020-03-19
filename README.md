# preseed-testing

## Procedure

Copy the desired preseed file to `custom.cfg`:

```shell
cp preseeds/preseed-ubuntu-18.04-server-regular-atomic.cfg custom.cfg
```

for a desktop installer

```shell
cp preseeds/preseed-ubuntu-18.04-desktop-regular-atomic.cfg custom.cfg
```

Then run the `build-and-run` script of your choice.

## How it works

Runs the custom.cfg preseed file against a VirtualBox VM in order to test an automated installation of an Ubuntu 18.04 server or desktop.

* Downloads ubuntu netinstall for Ubuntu 18.04
* Builds a custom install ISO
* Creates a VirtualBox VM
* Loads a custom preseed file called "custom.cfg"
* Runs the preseed file against the VM

## Requirements

Linux system. To test the generated iso file Virtualbox must be installed.

```shell
/usr/bin/vboxmanage
/usr/bin/xorriso
/usr/bin/7z
/usr/bin/sha1sum
```

## nvme drives

For installing to single or dual nvme drive you will want to execute the equivalent `build-and-run` script. Two rough examples are included, **build-and-run-dual-nvme-drives-test** and **build-and-run-nvme-drive**

For other drives use **build-and-run**

## Creating encrypted user passwords



```shell
openssl passwd -6 -salt xyz mypassword
```

## Creating a usb installer

Assuming usb stick is `/dev/sdc` and the pre-built image name is install.iso:

```
sudo dd bs=1M if=install.iso of=/dev/sdc
```

Alliteratively you can use the GUI **Disk Image Writer** by right clicking on the generated ISO and choosine **Open with Disk Image Writer**.

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

