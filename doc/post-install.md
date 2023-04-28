# Post Install
The instructions given below will guide you through the post installation procedure of installing Linux for MCSR.

# NVIDIA Drivers
- Before we proceed to install Minecraft and Java we need to first install the NVIDIA Drivers.
- If you are not on an NVIDIA GPU you can skip this section and proceed to the next one.
- When you boot into Mint, on the startup dialog, Go into **First Steps** section and scroll down and open the application named **Driver Manager**.
- It should automatically detect that you have an NVIDIA GPU and should suggest a list of drivers to install.
- The recommended option should be good enough. Click on the radio button to activate it and click on **Apply Changes** and enter your password as prompted.
- Now you can wait for the drivers to install and click on the **Restart** button to apply the changes.
- Remember! Do **NOT** install NVIDIA drivers from NVIDIA's official website. It creates some irreversible changes to the system that the package manager of Linux Mint cannot detect and might bloat your install with unnecessary packages. Moreover, everytime you need to update the driver, you would have to run through that process again. Whereas with the package manager, the driver updates will be rolled out after testing along with your normal upgrades. You can refer [here](https://forums.developer.nvidia.com/t/stop-asking-simple-users-to-install-the-unfriendly-run-file/48586) for more information.

# Java
- Before proceeding with anything from this point, go into **Update Manager** from either the startup dialog or by searching for the application as you would do on Windows.
- Make sure to update all the software pre-installed on the OS.
- After doing that, go into **Software Manager** either from the startup dialog or by searching for the application.
- In there, search for **openjdk-19-jdk** and download and install the package with the same name.
- This will install and setup the Java JDK for you.
- Remember! JDK versions will be named in the same format. So JDK 11 would be named as **openjdk-11-jdk** and so on. So if you want to install other versions of the JDK you follow the same format. Its easy, isn't it? :D

# MultiMC
- Download the .deb file for MultiMC from [here](https://multimc.org).
- It will be under the Linux downloads and the download link for **Debian/Ubuntu** is what we are looking for.
- After downloading it, locate to the file on the file manager and double click on the file and it will install MultiMC on your system for you.
- Now open MultiMC and login and create instances as per usual.
- Make sure to select the right Java version that you installed in the previous step from the list of auto detected Java installations. Linux Mint comes with a pre-installed Java version which is pretty outdated for Minecraft.

# OBS
- If you want to install OBS on your system, you can proceed with this section of the instructions.
- Go into **Software Manager** same as before and search for **OBS**.
- It will show you an application for OBS Studio with a **Flathub** icon under it.
- This is an official package from the OBS devs. There is another package named **obs-studio**. This is also another official package, but I haven't tested it out so it is recommended to install the **Flathub** version.
- After downloading and installing it, you can open it and set it up as per usual.
- OBS setup for **resetti** is detailed in the docs for **resetti**.

# Software Manager
- The software manager is the best place for you to search and install packages and apps.
- If you cannot find any package on it for some reason, Googling about it is your best friend. If Google doesn't have an answer for it too, then you can open an issue in [here](https://github.com/sathya-pramodh/linux-mcsr/issues/).

# resetti
- This is the Multi Instance macro we will be using on Linux.
- To install it, go [here](https://github.com/woofdoggo/resetti/releases/latest). Download the binary from the github release. If you are using Firefox (the default browser for Linux Mint) it should download the binary to the **Downloads** folder. If you download it elsewhere, replace **Downloads** with the path to that folder in the command given below. E.g: If you download it to your **Documents** folder, then your path would look something like **/home/<user_name>/Documents**.
- To update the binary, delete the binary from your **Downloads** folder and then go through the install process for **resetti** again.
- For more detailed install instructions with setup for OBS and everything, refer to the docs for **resetti** [here](https://github.com/woofdoggo/resetti).
- We are planning to add an auto-updating feature to the binary so you don't have to go through the process over and over again.
- To execute the macro, open a terminal window by hitting **Ctrl+Alt+T**. Now go into your **Downloads** folder by performing the following command (replace Downloads with the path you got from above if you downloaded the binary to another folder)
```
cd Downloads
```
- Now, set the executable flag to the binary by executing the following command. **NOTE: This has to be done only once(after an update or after the first download)**
```
chmod +x resetti
```
- Now, you can start the macro by doing this following command
```
./resetti <config_name>
```
- Here, replace **<config_name>** with the configuration name you want to use. All about the configuration of the macro is, again, given in the docs for **resetti** [here](https://github.com/woofdoggo/resetti/).
- If you have any questions, asking it in the [resetti discord](https://discord.gg/fwZA2VJh7k) is your best option.

# Update Cycle
- Linux Mint usually doesn't remind you or bug you to update your packages over and over.
- It has an update manager that reminds you if you have some major security updates pending.
- But if for some reason it misses it, then our recommendation is for you to follow a **monthly** update schedule, i.e., make sure to update all your packages by opening **Update Manager** on a monthly basis.
- This is just to make sure you don't run into any problems and to get the latest software for your system as early as possible.

# All done!
- Congratulations!! You just setup Linux for MCSR!! Happy resetting! :D
- Feel free to open an issue in [here](https://github.com/sathya-pramodh/linux-mcsr/issues) if you face any issues/problems while running your system. Good luck!
