# Boat Eye

Setting up boat eye on Linux is not as easy as it is on Windows. You might see some super weird behaviour while using it just because X11 handles mouse movement much different than Windows.

Make sure to follow instructions as closely as possible but if you do get any errors, make sure to post an issue [here](https://github.com/sathya-pramodh/linux-mcsr/issues) and I'll try and fix/debug the issue as far as possible.

The instructions given below will guide you through the procedure to setup boat eye on Linux.

# Flagged WMs

- There are quite many window managers that this setup would never work on. Here, we will just list all of them that I found people report about.
  - muffin (Linux Mint/Cinnamon Desktop Environment)
  - xfwm (XFCE Desktop Environment)
  - mutter (Gnome Desktop Environment)
  - kwin (KDE Desktop Environment)
- More will be added to this list as errors are reported.

# i3
i3 is a WM that has been tested a lot and it works very well with Fedora and all the tools. If you haven't setup i3 yet, you can do so in the **Setting up i3** section of this guide.

# Setting up mouse drivers

- Make sure that you have a Linux-compatible mouse (most Logitech and Razer mice should work. Make sure to check online if your mouse is Linux-compatible and is supported by any GUI software to configure DPI).
- Setup your mouse drivers by downloading the appropriate driver packages.
- Usually for Razer mice it is called `openrazer` for the GUI as well as the driver (I don't have a Razer mouse to cross-verify this. But do search around for the appropriate packages for your mouse).
- Usually for Logitech mice it is called `piper` for the GUI and `libratbag` for the driver package.
- After setting up your mouse drivers, make sure to open the GUI for setting up your mouse and check that your mouse is showing up on it.

# Cursor speeds and DPI

- First of all, install `xinput` from your distribution's packages. It is required for setting cursor speeds in X11.
- Refer to [Priffin's calculator](https://www.desmos.com/calculator/uld5u8glky) to figure out the proper boat eye cursor speed, DPI and sensitivity and setup any Minecraft related setup as explained [here](https://youtu.be/G5XNCcgv4qE).
  ![image](https://github.com/sathya-pramodh/linux-mcsr/assets/94102031/08041a38-7909-495f-b90f-b453b14152ce)
- To convert your cursor speeds to the appropriate multipliers (refer to the EPP off column here), use the table above.
- Set the DPI to the DPI that you took from the calculator in your mouse configuration application.
- Figure out the correct device ID for your mouse by running `xinput` in a terminal and analyzing the output.
- Pick the correct id corresponding to your mouse and note it down.
- Eg: `Logitech G102 LIGHTSYNC Gaming Mouse    	id=11	[slave  pointer  (2)]` Here the device id would be `11`.
- Now set the cursor speed by executing the following command in a terminal:

```bash
xinput set-prop <device_id> 'Coordinate Transformation Matrix' <multiplier> 0 0 0 <multiplier> 0 0 0 1
```

- Here, replace `<device_id>` with the id and `<multiplier>` with the multiplier that you took before well.
- Eg: `xinput set-prop 11 'Coordinate Transformation Matrix' 0.125 0 0 0 0.125 0 0 0 1 `

# wmctrl and xdotool

- wmctrl and xdotool are both command-line utilities used for desktop automation on Linux.
- Install `wmctrl` and `xdotool` from your distribution's packages.
- This will be required to be used along with `Autokey` in order to function as the Tall Macro.

# Autokey

- Autokey, a desktop automation tool, is required in order to run our Tall Macro script.
- Download `autokey` from your distribution's packages and open it.
- Hit `Ctrl+Shift+N` in order to create a new script.
- Enter the name that you want to give to the script on the left.
- Go to the script tab that has the contents `#Enter script code` in it.
- Paste in the below contents:

```python
#Enter script code
import os

zoom_w = 320 # Change this to the width you want Minecraft to be in after Tall Resolution is toggled on.
zoom_h = 16384 # Do not change this unless you know what you are doing.
zoom_x = 800 # Change this to the x coordinate you want Minecraft to go to when Tall Resolution is toggled on.
zoom_y = (1080 - zoom_h) // 2 # Do not change this unless you know what you are doing.

normal_w = 1920 # Change this to the width you want Minecraft to be in after Tall Resolution is toggled off.
normal_h = 1080 # Change this to the height you want Minecraft to be in after Tall Resolution is toggled off.
normal_x = 0 # Change this to the x coordinate you want Minecraft to go to when Tall Resolution is toggled off.
normal_y = 0 # Change this to the y coordinate you want Minecraft to go to when Tall Resolution is toggled off.

normal_multiplier = 0.125 # Change this to the multipler you took from the table.
zoom_multiplier = 0.03125 # Change this to your pleasing by referring to the table (default = 0.0315 = cursor speed 1).
device_id = 11 # Change this to the correct device id that you noted down before.

# Do not change anything after this!
os.system("xdotool getactivewindow getwindowgeometry | grep Geometry > /tmp/res")
f = open("/tmp/res")
cur_h = f.read().strip().split(':')[1].strip().split('x')[1]
f.close()

if(int(cur_h) == normal_h):
    if "Minecraft" in window.get_active_title():
        os.system(f"wmctrl -R ':ACTIVE:' -e 0,{zoom_x},{zoom_y},{zoom_w},{zoom_h}")
        os.system(f"xinput set-prop {device_id} 'Coordinate Transformation Matrix' {zoom_multiplier} 0 0 0 {zoom_multiplier} 0 0 0 1")

else:
    os.system(f"wmctrl -R ':ACTIVE:' -e 0,{normal_x},{normal_y},{normal_w},{normal_h}")
    os.system(f"xinput set-prop {device_id} 'Coordinate Transformation Matrix' {normal_multiplier} 0 0 0 {normal_multiplier} 0 0 0 1")
```

- Change the appropriate settings as indicated in the comments.
- Now go into the part that says `Hotkey` and click on the `Set` button.
- Now in the dialog box, click on `Record a key combination` and press the keys you would want to toggle Tall Resolution and click on `Ok`. This is usually just the `J` key.
- Now go into the part that says `Window Filter` and click on the `Set` button.
- Now in the dialog box, in the text box that says `Regular expression to match:` type in `Minecraft` and click on `Ok`.
- Now press the `Run Script` button and the hotkey should be activated. You can close the Autokey window now but it will still run in the system tray. You can suspend hotkeys by just right clicking on the systray entry for Autokey and hitting `Exit Autokey`.
- **NOTE:** You should run Autokey and run the script each time you want to have Tall Macro.
- You can also run custom scripts on every resolution toggle (eg. for setting DPI on toggling resolution for easier eye measurements by just adding a call to `os.system(<script_path>)` in the respective if/elif conditions, but this is out-of-scope of this document).

# Polling Rate

- Setting the polling rate to a lower value is nicer just because having a higher polling rate somehow affects how X11 behaves in response to specific cursor speeds.
- Open your mouse configuration GUI and search for the tab that configures the polling rate of your mouse. Make sure to set it to a low value (such as 250Hz).
- This is not a de-facto standard for all cursor speeds and it doesn't fix the issue for all mice. So if you have any issues please report it [here](https://github.com/sathya-pramodh/linux-mcsr/issues).

# Finishing Up

- The zoom overlay for pixel counting could also be setup the same way as Windows by using the method for non-Julti macros (using a screen capture on OBS).
- However, this version of the Tall Macro doesn't support moving the projector under the Tall Minecraft Window and displaying it alongside. But it is possible to have another screen where it is always open and just peeking over at that to count pixels.
- Congratulations! We have successfully setup boat eye on Linux!
