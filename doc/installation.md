# Installation

The instructions given below will install Fedora on your PC. Make sure to follow through the instructions here carefully.

# From Zero to Hero

- After testing out Fedora on the live environment, you are now ready to install it on your PC.
- You can connect to your home network in order to install some updates during the installation. But this is optional, you can proceed to install Fedora even without connecting to the internet.
- There are two options for you at this point. You can either
  - Have an empty hard drive to install Fedora on it.
  - Or have it be installed on your hard drive with Windows on it. (It will be installed alongside Windows so you need not worry. Just make sure you have enough space on that hard drive to have Fedora on it. Recommended size is about 100 GB of free space or above).
- No matter what you pick above most steps remain the same.
- Now on the Live Environment, search for **Install Fedora** by hitting the windows key and starting to type.
- The first menu will open up asking you to pick your language.
- Select your preferred language and click on **Continue**.
- In this menu you can click on **Time & Date** and change it (by clicking on the map) if it doesn't show the right timezone for you (usually doesn't if you aren't connected to the internet).
- You can also click on **Keyboard** to change the layout that you want to use (if it hasn't detected it correctly).

## Installation Destination 

- Click on the **Installation Destination** icon under the **SYSTEM** option.
- The option you selected above matters only here. Be very sure that you have plugged in the right disks for installation. A gentle reminder to check and re-check them right now before continuing.
  - If you chose to install Fedora on a separate empty hard drive, you will have that har drive directly listed under **Local Standard Disks**. You can click on it if it doesn't have a tick mark under it and click on the **Continue** button.
  - If you chose to install Fedora alongside your Windows install, you will have to select the **Custom** option under **Storage Configuration** and hit the **Continue** button. Now you will be redirected to a new GUI where you can click on the drop down that says **Btrfs** and select **ext4** instead. Now click on **Click here to create them automatically** and the installer will try to do it automatically for you. Then click on the **Done** button.

# Continuation of Installation

- Click on **Begin Installation** and the installation of Fedora onto whatever disk/partition you chose will begin.
- Once it is done, click on the **Finish Installation** button. This will close the installer.
- Then you can click on the top right status tray and click on the power button to reboot the system. Make sure to reboot with the USB removed.
- After rebooting, you will be prompted to **Start Setup** and setup your username and password.
- Make sure to also enable third-party repositories during the setup. This will be required to install some software that might be proprietary but you might need them on a daily basis.
- Now logout of the system, and in the login screen click on the cog icon and choose the option that says **GNOME on Xorg** as Fedora defaults to a Wayland session on the first boot and [resetti](https://github.com/tesselslate/resetti) doesn't function on Wayland as of now. Now you can log back into your system.
- Also make sure to update your system as soon as you log back in by running the command `sudo dnf update` in a terminal.

Your Linux installation is now complete! We can now proceed with the post installation configuration.
