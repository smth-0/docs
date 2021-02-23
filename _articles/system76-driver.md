---
layout: article
title: Install the System76 Driver
description: >
    Our System76 Driver can generate system logs, we'll also go over how to reinstall the NVIDIA Driver.
keywords:
  - system76
  - driver
  - NVIDIA
  - support
image: http://support.system76.com/images/system76.png
hidden: false
section: hardware-drivers

---

# Ubuntu and Pop!_OS

## Apt Preferences File

If you are running Ubuntu 19.10 or later, you will need to manually add an apt preferences file to "pin" the System76 repository. This will tell apt to prefer System76 packages over standard Ubuntu packages. Installing the System76 Driver will not be possible until this step is completed.

Create the apt preferences file here:

```
sudo gedit /etc/apt/preferences.d/system76-apt-preferences
```

Add the following six lines (seven if you count the space in the middle):

```
Package: *
Pin: release o=LP-PPA-system76-dev-stable
Pin-Priority: 1001

Package: *
Pin: release o=LP-PPA-system76-dev-pre-stable
Pin-Priority: 1001
```

Save the file. Now you should be able to install the System76 Driver as described below.

To install our Driver you need to run the following commands in the Terminal:

```
sudo apt-add-repository -y ppa:system76-dev/stable
sudo apt-get update
sudo apt-get install -y system76-driver
```

## Generate Log Files

The System76 Driver can be opened by pressing the Ubuntu or Pop key and then search for 'system76', then click on the System76 Driver. 

Next click on the button outlined in red in the <u>System76 Driver</u> application and there will be a file called `system76-logs.tgz` placed in your Home directory (/home/username)

![CreateLogFiles](/images/system76-driver/CreateLogFiles.png)

### System76 NVIDIA Driver

Follow the above steps as well as this additional command if you have a NVIDIA GPU:

```
sudo apt-get install system76-driver-nvidia
```

### Arch Linux (Arch-based Distros):

### Tested on the following systems 
- Base Manjaro GNOME install     
- Base Arch GNOME install         

### Packages needed:

Using the AUR for system76 packages:

```
sudo pacman -S --needed base-devel git linux-headers
```

---
**NOTE**
  For Manjaro make sure to match with the kernel version. Manjaro offers several kernels including the latest stable and LTS versions. You can use this command to find the kernel version:

```
uname -r
```

For any GNOME Shell extensions to show up in the Extensions application you will need to log out and back in.

## Build and Install system76-firmware

#### Download PKGBUILD:

```
git clone https://aur.archlinux.org/system76-firmware.git
```

#### Run these commands:

```
cd system76-firmware-daemon
makepkg -srcif
```
 
#### Now to enable and start the service:

```
sudo systemctl enable --now system76-firmware-daemon
```

## Build and Install firmware-manager

#### Download PKGBUILD:

```
git clone https://aur.archlinux.org/firmware-manager.git
```

#### Run these commands:

```
cd firmware-manager
makepkg -srcif
```

---

These packages need to be installed in this order for them to complete their build and install processes.

### Build and Install system76-dkms

#### Download PKGBUILD:

```
git clone https://aur.archlinux.org/system76-dkms.git
```

#### Run these commands:

```
cd system76-dkms
makepkg -srcif
```

### Build and Install system76-power

#### Download PKGBUILD:

```
git clone https://aur.archlinux.org/system76-power.git
```

#### Run these commands:

```
cd system76-power
makepkg -srcif
sudo systemctl enable --now system76-power
```

**NOTE**

 If you are using a NVIDIA graphics card, you may need to add additional
    X11 config to make the GPU switching work, see below:

        https://wiki.archlinux.org/index.php/NVIDIA_Optimus#Use_NVIDIA_graphics_only

### Build and Install gnome-shell-extension-system76-power

#### Download PKGBUILD:

```
git clone https://aur.archlinux.org/gnome-shell-extension-system76-power-git.git
```

#### Run these commands:

```
cd gnome-shell-extension-system76-power
makepkg -srcif
```

## Build and Install system76-driver

**NOTE**
The package is currently is out of date.

#### Download PKGBUILD:

```
git clone https://aur.archlinux.org/system76-driver.git
```

#### Run these command:

```
cd system76-driver
makepkg -srcif
sudo systemctl enable --now system76
```

## Build and Install system76-io-dkms 
(this is only needed for the Thelio Io board)

#### Download PKGBUILD:

```
git clone https://aur.archlinux.org/system76-io-dkms.git
```

#### Run these commands:

```
cd system76-io-dkms
makepkg -srcif
```

## Build and Install system76-acpi-dkms

#### Download PKGBUILD:

```
git clone https://aur.archlinux.org/system76-acpi-dkms.git
```

#### Run these commands:

```
cd system76-acpi-dkms
makepkg -srcif
```

## Build and Install system76-oled 
(this is only needed for systems with OLED panels like the addw1/addw2)

#### Download PKGBUILD:

```
git clone https://aur.archlinux.org/system76-oled.git
```

#### Run these commands:

```
cd system76-acpi-oled
makepkg -srcif
```
