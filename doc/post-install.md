# Post Install
The instructions given below will guide you through the post installation procedure of installing Linux for MCSR.

# Linux Terminal
- To use Linux on the Desktop casually, you wouldn't need to know the terminal at all.
- But to setup MCSR, we will have to go through some basic commands and how they work.
- You can skip this altogether though and just blindly follow the instructions, but to debug stuff better, it is better to know these basics.
- To learn about the basics of the Linux commandline proceed to [here](https://github.com/sathya-pramodh/linux-mcsr/blob/main/doc/terminal.md).
- It also has some basic scripting examples with two scripts that you can use to make your life easier with MCSR.

# NVIDIA Drivers
- Before we proceed to install Minecraft and Java we need to first install the NVIDIA Drivers.
- If you are not on an NVIDIA GPU you can skip this section and proceed to the next one. You can still check in here to see if you have additional proprietary drivers that you might need to install.
- When you boot into Mint, on the startup dialog, Go into **First Steps** section and scroll down and open the application named **Driver Manager**.
- It should automatically detect that you have an NVIDIA GPU and should suggest a list of drivers to install.
- The recommended option should be good enough. Click on the radio button to activate it and click on **Apply Changes** and enter your password as prompted.
- Now you can wait for the drivers to install and click on the **Restart** button to apply the changes.
- Remember! Do **NOT** install NVIDIA drivers from NVIDIA's official website. It creates some irreversible changes to the system that the package manager of Linux Mint cannot detect and might bloat your install with unnecessary packages. Moreover, everytime you need to update the driver, you would have to run through that process again. Whereas with the package manager, the driver updates will be rolled out after testing along with your normal upgrades. You can refer [here](https://forums.developer.nvidia.com/t/stop-asking-simple-users-to-install-the-unfriendly-run-file/48586) for more information.
- Also **NOTE:** If you are using the driver version greater than 525, make sure to add `env __GL_THREADED_OPTIMIZATIONS=0` to your wrapper command alongside whatever you add with jemalloc (from resetti docs down below) as with driver versions greater than 525, preemptive doesn't seem to function as intended because of a driver-side optimization to the Minecraft renderer. Eg: `env __GL_THREADED_OPTIMIZATIONS=0 $INST_JAVA` would be an example of the wrapper command.

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
- To install it, go [here](https://github.com/woofdoggo/resetti/releases/tag/v0.5.2-beta). Download the binary from the github release. If you are using Firefox (the default browser for Linux Mint) it should download the binary to the **Downloads** folder. If you download it elsewhere, replace **Downloads** with the path to that folder in the command given below. E.g: If you download it to your **Documents** folder, then your path would look something like `/home/<user_name>/Documents`.
- To update the binary, delete the binary from your **Downloads** folder and then go through the install process for **resetti** again.
- For more detailed install instructions with setup for OBS and everything, refer to the docs for **resetti** [here](https://github.com/woofdoggo/resetti).
- We are planning to add an auto-updating feature to the binary so you don't have to go through the process over and over again.
- To execute the macro, open a terminal window by hitting `Ctrl+Alt+T`. Now go into your **Downloads** folder by performing the following command (replace Downloads with the path you got from above if you downloaded the binary to another folder)
```bash
cd Downloads
```
- Now, set the executable flag to the binary by executing the following command. **NOTE: This has to be done only once(after an update or after the first download)**
```bash
chmod +x resetti
```
- Now, you can start the macro by doing this following command
```bash
./resetti <config_name>
```
- Here, replace **<config_name>** with the configuration name you want to use. All about the configuration of the macro is, again, given in the docs for **resetti** [here](https://github.com/woofdoggo/resetti/).
- If you have any questions, asking it in the [resetti discord](https://discord.gg/fwZA2VJh7k) is your best option.

# NinjabrainBot
- Download the .jar for NinjabrainBot as per usual from [here](https://github.com/Ninjabrain1/Ninjabrain-Bot/releases/latest).
- Lets take an example where the .jar file is downloaded into the **Downloads** folder.
- Now to add it as an application to your list of applications, create this file with the following contents under `~/.local/share/applications/NinjabrainBot.desktop`
```bash
[Desktop Entry]
Encoding=UTF-8
Type=Application
Name=NinjabrainBot
Icon=minecraft
Exec=java -jar /home/<user_name>/Downloads/Ninjabrain-Bot-1.4.1.jar
```
- If the directory does not exist, then make the directory/directories by executing the following command in a terminal
```bash
mkdir -p ~/.local/share/applications/
```
- Remember that the file name will change over versions. So as you update Ninjabrain Bot, you will have to change this file as well. Also, you will have to replace `<user_name>` with your username that you set during the install.
- If you downloaded it elsewhere, then replace `/home/<user_name>/Downloads/Ninjabrain-Bot-1.4.1.jar` with the relevant path.
- Now you can launch Ninjabrain Bot from your applications menu!

# Boat Eye
- Setting up boat eye on Linux is not as easy as it is on Windows. You might see some super weird behaviour while using it just because X11 handles mouse movement much different than Windows.
- Make sure to follow instructions as closely as possible but if you do get any errors, make sure to post an issue [here](https://github.com/sathya-pramodh/linux-mcsr/issues) and I'll try and fix/debug the issue as far as possible.
- Go [here](https://github.com/sathya-pramodh/linux-mcsr/blob/main/doc/boat-eye.md) to continue with boat eye setup.

# ModCheck
- Download the .jar for ModCheck as per usual from [here](https://github.com/RedLime/ModCheck/releases/latest)
- Lets take an example where the .jar file is downloaded into the **Downloads** folder.
- Now to add it as an application to your list of applications, create this file with the following contents under `~/.local/share/applications/ModCheck.desktop`
```bash
[Desktop Entry]
Encoding=UTF-8
Type=Application
Name=NinjabrainBot
Icon=minecraft
Exec=java -jar /home/<user_name>/Downloads/ModCheck-0.6.jar
```
- If the directory does not exist, then make the directory/directories by executing the following command in a terminal
```bash
mkdir -p ~/.local/share/applications/
```
- Remember that the file name will change over versions. So as you update ModCheck, you will have to change this file as well. Also, you will have to replace `<user_name>` with your username that you set during the install.
- If you downloaded it elsewhere, then replace `/home/<user_name>/Downloads/ModCheck-0.5.3.jar` with the relevant path.
- Now you can launch ModCheck from your applications menu!

# Micro Optimizations
## Jemalloc setup for better Minecraft Performance
- To install `jemalloc` on Linux Mint as guided [here](https://github.com/woofdoggo/resetti/blob/main/doc/troubleshooting.md#improving-malloc-performance), open up a terminal and type in the command `sudo apt install libjemalloc-dev` and type in the password as prompted.
- This should setup jemalloc for you. Just make sure to add the wrapper commands as guided in resetti's docs.

## GLFW Setup to prevent BadWindow crashes.
- To install `glfw` for Linux Mint as guided [here](https://github.com/woofdoggo/resetti/blob/main/doc/common-issues.md#building-glfw-from-source), go into the **Software Manager** and search for **glfw** and install the first package that shows up.
- This should setup glfw for you. Using system installation of glfw for each Minecraft instance in MultiMC by going into `Edit Instance` -> `Settings` -> `Workarounds` -> `Use system installation of GLFW`
- Or you can compile and build GLFW from source and follow the instructions [here](https://github.com/woofdoggo/resetti/blob/main/doc/common-issues.md#building-glfw-from-source).

## Setting up tmpfs
- You might get slightly better performance while running wall by symlinking your instance world folders into `/tmp/mc/`.
- First run this following command to create the `mc` directory in `/tmp`
```bash
mkdir -p /tmp/mc/
```
- E.g. While running PrismLauncher (a fork of MultiMC), I would symlink `~/.local/share/PrismLauncher/instances/Instance1/.minecraft/saves` to `/tmp/mc/1/` and so on by using the command below for each
```bash
ln -s  /tmp/mc/1 ~/.local/share/PrismLauncher/instances/Instance1/.minecraft/saves
```
- And now you can keep clearing out this folder every 300s or so by running a simple script in the background.
- The script would look something like this
```bash
#!/bin/bash
cd /tmp/mc
while true
    do 
        for i in {1..15}
        do 
            cd $i && rm -r $(ls -t1 | tail -n 20) && cd ..
        done
        sleep 300
    done
```
- Here the last number in the for loop is the total number of instances that you have. Make sure to name the folders exactly as in the above example for this script, i.e., `/tmp/mc/1` and so on.
- Now set the executable flag on the script by performing the following command in a terminal
```bash
chmod +x script.sh
```
- And execute it everytime you start your resetting session with the following command 
```bash
./script.sh
```
- **NOTE: Use this method IF AND ONLY IF you have some RAM to spare with all the instances running and resetting. DO NOT use it if you are using >70-80% of RAM during resetting as running that script in the background takes up memory as well!**

# Rebinding Keys (for bookcrafting)
- Install `xdotool` and `xbindkeys` from the **Software Manager** by searching for them.
- Now edit the file name `.xbindkeysrc` in your home directory (shorthanded with `~`) and add these lines inside the file to rebind the one key to the other
```
"xdotool key '<Rebound key combination>'"
    release+'<Original key combination>'
```
- E.g: If you want to rebind `r` to `6` then you would add these lines
```
"xdotool key '6'"
    release+r
```
- You can just read the examples given in the file to understand clearly how to do it for a modifier setup or for binding a combination of keys.
- Now run the following command in a terminal to background the process and bind all the keybinds set in `.xbindkeysrc`
```bash
xbindkeys
```
- If you don't want to background the xbindkeys process (useful for debugging), then execute the following command
```bash
xbindkeys -v
```
- Note that you need to do one of these above commands in a terminal before you start your resetting session.

# Splitting audio on Linux for OBS
- Splitting audio on Linux using Virtual Audio inputs is always a pain to do. 
- If you are ready to get this setup, go [here](https://github.com/sathya-pramodh/linux-mcsr/blob/main/doc/splitting-audio.md).

# Update Cycle
- Linux Mint usually doesn't remind you or bug you to update your packages over and over.
- It has an update manager that reminds you if you have some major security updates pending.
- But if for some reason it misses it, then our recommendation is for you to follow a **monthly** update schedule, i.e., make sure to update all your packages by opening **Update Manager** on a monthly basis.
- This is just to make sure you don't run into any problems and to get the latest software for your system as early as possible.

# All done!
- Congratulations!! You just setup Linux for MCSR!! Happy resetting! :D
- Feel free to open an issue in [here](https://github.com/sathya-pramodh/linux-mcsr/issues) if you face any issues/problems while running your system. Good luck!
