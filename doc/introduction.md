# Introduction

The instructions given below will be the pre-install setup. By the end of it, you will have a bootable USB stick with Fedora installed on it.

# Distributions

- Linux, being a **free and open source operating system**, comes in several different flavours a.k.a distributions a.k.a distros.
- Some of the popular distributions are **Ubuntu**, **Fedora**, **Arch Linux(btw)**, etc.
- For MCSR, we recommend a distribution based on **RHEL** called **Fedora**.
- Make sure to go [here](https://fedoraproject.org/workstation/download) and download the latest ISO for Fedora.
- Click on the ISO file under **For Intel and AMD x86_64 systems**. This is what we will be using to flash the USB.
- You can learn more about **Linux Distributions** [here](https://en.wikipedia.org/wiki/Linux_distribution).

# Installing Fedora Workstation 

- After downloading the distribution ISO from the official Fedora Project website, pick up a USB stick of at least 5GB space or above.
- **NOTE: The USB stick will be formatted during the install process and all data on it will be erased.**
- To install the ISO into the USB stick, use **Balena Etcher** from [here](https://www.balena.io/etcher#download-etcher). Click on the Windows installer link to download it.
- Run through the Balena Etcher installer as per usual.
- Plug in the USB stick to your PC and open Balena Etcher.
- Under **Select Image**, locate to wherever you downloaded the Fedora Workstation ISO from before and select it.
- Under **Select Drive**, select the USB device name. It should be auto-selected for you, just make sure its the right USB.
- Then click **Flash** to start creating your Bootable USB!
- Wait for it to finish **Flashing** and **Verifying** as well. Don't quit Balena until all of it is done.
- Congratulations! You just created a bootable Fedora USB!

# Moving Ahead

- Make sure to have Secure Boot disabled in your motherboard settings and make sure to have CSM/BIOS mode disabled before you proceed to other sections.
- Now we start with the difficult part of the installation. We make decisions based on your PC configuration. So make sure to follow through the instructions very carefully.
