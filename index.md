# No Kernel Headers were found! Skipping Module Build

Welcome to my blog!

In this post, I’ll walk you through how I fixed the VirtualBox kernel issue on Linux.

---

## Problem
While installing VirtualBox, I encountered this error:
*“No Kernel Headers were found! Skipping Module Build"*

---

## Solution
To get the headers for the running kernel kindly install the kali headers package


## Steps to Fix
1. Updated my system:
sudo apt update && sudo apt upgrade -y

2. Installed required packages:
sudo apt install -y linux-headers-$(uname -r) build-essential dkms

If linux-headers-$(uname -r) gives package not found, it means the headers for your kernel aren’t in the repos yet. 
In that case, you may need to upgrade your kernel to a version with headers available then Reboot:
sudo apt install -y linux-image-amd64 linux-headers-amd64

3. Reinstalled VirtualBox modules:
sudo apt install --reinstall virtualbox-dkms virtualbox

4. Loaded the kernel modules:
sudo modprobe vboxdrv
sudo modprobe vboxnetflt
sudo modprobe vboxnetadp

5. Checked the VirtualBox service:
systemctl status virtualbox.service
If it’s inactive/failed, restart it:
sudo systemctl restart virtualbox.service
6. Launched VirtualBox again:
virtualbox

If everything is correct, the /dev/vboxdrv device will now exist and you’ll be able to start VMs.
