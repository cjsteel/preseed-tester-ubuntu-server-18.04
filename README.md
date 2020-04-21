# preseed-tester

## Procedures

### Paradox

You may want a fully automated installation image, but, most people do not for both practical and safety reasons. By not including or otherwise breaking the preseed files' networking  and/or the OS installation target disk will results in a user prompt for networking information and/or selection the the target disk for installation. This is very helpful in many situations when  you want a single installer to against many systems as IP addresses are always different and target device names change on some systems in certain situations.

In all of these cases, not having a fully automated installer is a significantly more efficient and pragmatic way to get more done with less effort.

### Testing

By default the included scripts will attempt to test your new installer using a local version of VirtualBox. Always a good idea. That said, If you do not have a local installation of VirtualBox the script will still generate an installer ISO (as well as a few error messages).

### Included preseed examples

Preseed files for Ubuntu 18.04 Server and Workstation are included in the `preseed` directory.

#### User configuration

The included preseed files' with create a user: **julie** with an encrypted password: **mypassword**. Don't forget to ecrypt any password you change or it will not work

```shell
openssl passwd -6 -salt xyz mypassword
```

#### Additional customizations to OS

Near the end of each preseed file additional customizations to the target OS can be made. You might want to keep the final command to shut the system down after the installation is completed until you are certain that your installation process is successful in installing, configuring and securing your system.

### custom.cfg

`custom.cfg` is the preseed that is added to the *.iso installer image

## Creating a custom ISO installer

### preseed customizations

* Create or copy and edit a preseed in the `preseeds` directory.

#### Update `custom.cfg`

* Copy your custom preseed file to `custom.cfg`.

#### Create and test a custom ISO

* Execute one of the **build-and-run** scripts.

#### Real world example

##### Select your preseed

To create an Ubuntu 18.04 Server "atomic" installer

```shell
cp preseeds/preseed-ubuntu-18.04-server-regular-atomic.cfg custom.cfg
```

To create an Ubuntu 18.04 Workstation "atomic" installer

```shell
cp preseeds/preseed-ubuntu-18.04-desktop-regular-atomic.cfg custom.cfg
```

##### build and test your installer ISO

```shell
./build-and-run-nvme-drive
```

##### Create a usb installer

Once you are satisfied with the test results you can create and installation USB or use your ISO in some other way.

Create usb installer from command line

From the project directory and assuming usb stick is `/dev/sdc` and the pre-built image name is Ubuntu-18.04.2-server-680d82a-unattended.iso:

```
sudo dd bs=1M if=Ubuntu-18.04.2-server-680d82a-unattended.iso of=/dev/sdc
```

Alliteratively you can use the Ubuntu GUI **Disk Image Writer** by right clicking on the generated ISO and choosing **Open with Disk Image Writer**.

## How it works

Runs the custom.cfg preseed file against a VirtualBox VM in order to test an automated installation of an Ubuntu 18.04 server or desktop.

* Downloads Ubuntu net installer for Ubuntu 18.04

* Builds a custom install ISO

  * Includes a copy of the custom.cfg preseed file

* Runs resulting ISO installer against a VirtualBox VM

  * Creates a VirtualBox VM

  *  Runs the installer against the VM

## Requirements

* Linux and some ISO utilities

* VirtualBox if you want to test your image

```shell
sudo apt install xorriso
sudo apt-get install p7zip-full
which sha1sum # comes with many distros
```

```shell
/usr/bin/vboxmanage
/usr/bin/xorriso
/usr/bin/7z
/usr/bin/sha1sum
```

## nvme drives

For installing to single or dual nvme drive you will want to execute the equivalent `build-and-run` script. Two rough examples are included, **build-and-run-dual-nvme-drives-test** and **build-and-run-nvme-drive**

I almost always use one of the **nvme** scripts for testing and production. For production installers where you want a fully automated install you might want to use **build-and-run** 

## Ubuntu LTS installer documentation

install methods:

1. Ubiquity installer (which is a fairly limited install from a pre-built complete system 
   image).
2. Network install using [Debian Installer][1].

This customized installer is the "Debian installer" flavour. Best place for documentation
is Debian docs.

[1]: https://wiki.debian.org/DebianInstaller/

## Source

* Cloned from https://github.com/tadas-s/custom-ubuntu-install and modified

