---
title: VirtualBox
summary: Quick start guide for VirtualBox on Solus
---

# VirtualBox

[VirtualBox](https://www.virtualbox.org/) is an x86 and x86_64 virtualization software package developed by Oracle.

## Before you start

This section applies to new installations for both **Host** and **Guest**.

### Remove prior installation

It is important to uninstall any version of VirtualBox (or VirtualBox Guest Additions) that **was not** installed from the Software Center or there will be conflicts that will prevent the application to work.
This can usually be done by executing the following command from a terminal:

```bash
sudo /opt/VirtualBox/uninstall.sh
```

### Update your system

Ensure your system is up-to-date. This is very important because VirtualBox installs some kernel modules and the application will not work if your kernel is outdated.

```bash
sudo eopkg upgrade
```

### Determine which kernel you are using

Solus support both a `current` and `lts` kernel. It is important to install the version that corresponds to your kernel.

If you aren't sure which kernel you are running, run the following in terminal:

```bash
uname -r
```

You will either have a `.current` or `.lts` suffix. Examples: `5.13.1-187.current` or `4.14.237-175.lts`

## Solus as host

VirtualBox is available in the Software Center, select the package that matches your kernel.

| virtualbox                                           | virtualbox-current                                       |
| ---------------------------------------------------- | -------------------------------------------------------- |
| VirtualBox host modules for the **linux-lts** kernel | VirtualBox host modules for the **linux-current** kernel |

You **must** reboot your computer before running VirtualBox for the first time.

## Solus as guest

VirtualBox Guest Additions are available in the Software Center, select the package that matches kernel version on the Solus virtual machine.

| virtualbox-guest                                      | virtualbox-guest-common                                      |
| ----------------------------------------------------- | ------------------------------------------------------------ |
| VirtualBox guest modules for the **linux-lts** kernel | Install this package if the **linux-current** kernel is used |

You **must** reboot your virtual machine to load the newly installed modules

## Extra configuration

#### USB controller

If you want to use USB 2.0 or 3.0 in your virtual machine (and your hardware supports it), you have to install the [extension pack](https://www.virtualbox.org/manual/ch01.html#intro-installing).

Note: Access to USB is granted by the user group `vboxusers` on the **Host** operating system. You can add yourself to this group with the following command

```bash
sudo gpasswd -a $USER vboxusers
```

#### Shared folders

Share folders let you access files from the host system from within a guest machine.

**Note:** auto-mounted shared folders are mounted into the `/media` directory, along with the prefix `sf_`. For example, the shared folder `myfiles` would be mounted to `/media/sf_myfiles`.

Access to the shared folders is only granted to the user group `vboxsf` on the **Guest** operating system.

Execute these commands to set the permissions and add yourself to the group

```bash
sudo gpasswd -a $USER vboxsf
```

## Troubleshooting

![VBOX Kernel](./vbox-kernel.png)

The Error `Kernel driver not installed (rc=-1908)` may occur if

- The computer was not restarted before launching VirtualBox for the first time
- The computer is not booted on the latest kernel. Make sure to apply the updates from the Software Center and restart your machine.
- The wrong VirtualBox package was installed. Please check the instructions just above to install the correct package for your kernel.
- VirtualBox was manually installed and it conflicts with the version installed from the Solus Repository.
