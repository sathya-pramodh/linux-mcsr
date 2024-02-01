# NVIDIA Drivers

- Before we proceed to install Minecraft and Java we need to first install the NVIDIA Drivers.
- If you are not on an NVIDIA GPU you can skip this section and proceed to the next one. You can still check in here to see if you have additional proprietary drivers that you might need to install.
- When you boot into Mint, on the startup dialog, Go into **First Steps** section and scroll down and open the application named **Driver Manager**.
- It should automatically detect that you have an NVIDIA GPU and should suggest a list of drivers to install.
- The recommended option should be good enough. Click on the radio button to activate it and click on **Apply Changes** and enter your password as prompted.
- Now you can wait for the drivers to install and click on the **Restart** button to apply the changes.
- Remember! Do **NOT** install NVIDIA drivers from NVIDIA's official website. It creates some irreversible changes to the system that the package manager of Linux Mint cannot detect and might bloat your install with unnecessary packages. Moreover, everytime you need to update the driver, you would have to run through that process again. Whereas with the package manager, the driver updates will be rolled out after testing along with your normal upgrades. You can refer [here](https://forums.developer.nvidia.com/t/stop-asking-simple-users-to-install-the-unfriendly-run-file/48586) for more information.
- Also **NOTE:** If you are using the driver version greater than 525, make sure to add `env __GL_THREADED_OPTIMIZATIONS=0` to your wrapper command alongside whatever you add with jemalloc (from resetti docs down below) as with driver versions greater than 525, preemptive doesn't seem to function as intended because of a driver-side optimization to the Minecraft renderer. Eg: `env __GL_THREADED_OPTIMIZATIONS=0 $INST_JAVA` would be an example of the wrapper command.
