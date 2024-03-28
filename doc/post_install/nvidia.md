# NVIDIA Drivers

- Before we proceed to install Minecraft and Java we need to first install the NVIDIA Drivers.
- If you are not on an NVIDIA GPU you can skip this section and proceed to the next one. You can still check in here to see if you have additional proprietary drivers that you might need to install.
- Open up a terminal and then type in these commands.
```bash
sudo dnf install kernel-devel kernel-headers gcc make dkms acpid libglvnd-glx libglvnd-opengl libglvnd-devel pkgconfig
sudo dnf install https://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
sudo dnf makecache
sudo dnf install akmod-nvidia xorg-x11-drv-nvidia-cuda
```
- This should install nvidia drivers on your system. Now you can restart your system and you should have GPU acceleration. Report any issues [here](https://github.com/sathya-pramodh/linux-mcsr/issues).
- Remember! Do **NOT** install NVIDIA drivers from NVIDIA's official website. It creates some irreversible changes to the system that the package manager of Fedora cannot detect and might bloat your install with unnecessary packages. Moreover, everytime you need to update the driver, you would have to run through that process again. Whereas with the package manager, the driver updates will be rolled out after testing along with your normal upgrades. You can refer [here](https://forums.developer.nvidia.com/t/stop-asking-simple-users-to-install-the-unfriendly-run-file/48586) for more information.
- Also **NOTE:** If you are using the driver version greater than 525, make sure to add `env __GL_THREADED_OPTIMIZATIONS=0` to your wrapper command alongside whatever you add with jemalloc (from resetti docs down below) as with driver versions greater than 525, preemptive doesn't seem to function as intended because of a driver-side optimization to the Minecraft renderer. Eg: `env __GL_THREADED_OPTIMIZATIONS=0 $INST_JAVA` would be an example of the wrapper command.
