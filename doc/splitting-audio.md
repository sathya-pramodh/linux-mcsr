# Splitting audio
In this document we will be setting up Virtual Audio Inputs and splitting audio outputs in OBS. Remember! This method is highly untested and it works very well on my PC at the moment. But if you have any issues, post it [here](https://github.com/sathya-pramodh/linux-mcsr/issues).

# qpwgraph
- This is the app that will let us split audio easily with a GUI.
- You can download it by executing this in your terminal
```
sudo apt install qpwgraph
```
- We now need to setup `qpwgraph` such that it launches each time with the correct arguments on startup.
- Copy the following contents into a file named `qpwgraph.desktop` and drop it in `~/.config/autostart/`.
```
[Desktop Entry]
Name=qpwgraph
Version=1.0
GenericName=PipeWire Graph/Patchbay
Comment=qpwgraph is a PipeWire graph Qt GUI interface
Exec=qpwgraph %f -axm
Icon=org.rncbc.qpwgraph
Categories=AudioVideo;Audio;Video;Midi;X-Alsa;X-PipeWire;Qt;
MimeType=application/x-qpwgraph-patchbay;
Keywords=PipeWire;MIDI;ALSA;JACK;Qt;
Terminal=false
Type=Application
```
- We will be using this application later on to setup output routing.
- **NOTE**: If you are using a window manager though, make sure to add `qpwgraph -axm` to your autostart script for your window manager.

# Setting up Virtual Audio Cables
- We setup virtual audio cables by using a script that launches each time you login to your system.
- Copy the following contents into a file named `virtual_inputs` and in a terminal execute `chmod +x virtual_inputs` to make it executable and then move the file into `/usr/bin`.
```bash
#!/bin/sh
pactl load-module module-null-sink media.class=Audio/Sink sink_name=Virtual_Input_1
pactl load-module module-null-sink media.class=Audio/Sink sink_name=Virtual_Input_2
```
- If you don't have the `pactl` command you can install it by executing `sudo apt install pactl`.
- The above script is to make 2 virtual inputs which are more than enough to do basic audio splitting. You can add more by just copying and pasting these lines and changing the `sink_name` to `Virtual_Input_3` and so on.
- Now we can setup `virtual_inputs` to launch on startup.
- Copy the following contents into a file named `virtual_inputs.desktop` and drop it in `~/.config/autostart/`.
```
[Desktop Entry]
Encoding=UTF-8
Type=Application
Exec=virtual_inputs
Terminal=false
Name=Virtual Inputs
```
- Now you can logout and login to your system and see that an icon is added to your taskbar at the very right.
- **NOTE**: If you are using a window manager though, make sure to add `virtual_inputs &` to your autostart script for your window manager.

# Setting up OBS
- We setup OBS now to add two JACK Audio Inputs which will take the outputs from the virtual audio cables and splits it out.
- Go into your OBS Settings and disable `Desktop Audio` from the `Audio` tab by selecting `Disabled` against the `Desktop Audio` option.
- In each of your `Wall` and `Instance` scenes, click on the `+` icon and add a `JACK Input Client` and name it `Desktop Audio` and `Spotify`.
- Accept the defaults on the `JACK Input Client`.

# Setting up Audio Splits
- Open up qpwgraph.
- Connect your audio outputs to the virtual inputs. 
- Connect your spotify output to any of the virtual input as well by connecting the left and right outputs to the left and right inputs respectively. You can get it visible in the graph by opening up spotify and playing any music.
- Make sure to also route your Virtual Input Devices to the physical output device that you would like to use. For example your headphones.
- Make sure to route `Built-in Audio Analog Stereo` captures or your Mic captures to your `OBS [Mic/Aux]` input. It might be done automatically but sometimes it might need a little fixing.
- Now you can route the virtual inputs to your OBS JACK inputs. It will be usually named something like `OBS Studio: Desktop Audio` and `OBS Studio: Spotify`.
- As a convention, you can use `OBS Studio: Spotify` to be the one that doesn't get published to the VoD and `OBS Studio: Desktop Audio` to be published to the VoD.
- You can set this up by going into your `Advanced Audio Settings` and then routing which audio streams `Desktop Audio` and `Spotify` go to and you can enable `Twitch VoD Track` from the `Output` tab.
- Now hit `Ctrl + S` to save changes in qpwgraph. If this somehow doesn't work, you can try qutting the application by right clicking on the taskbar icon and choosing `Exit`. It should prompt you to save it as something. Save it giving it any name you choose and close.
- Now qpwgraph should startup each time you login with that graph applied, so the audio connections would be made automatically as the instances, OBS and spotify launch. 
- Sometimes with the Spotify desktop app you might have some issues with the connections flickering from one Virtual Input to the other. If so, please post an issue [here](https://github.com/sathya-pramodh/linux-mcsr/issues).
- Now go into your Linux Mint settings and go into the `Audio` settings tab and set the current audio device that you are using to be any of the virtual inputs that you want. Mind you, this step is done because you would want all your game audio to be routed to that virtual input because the audio outputs of Minecraft gets re-routed each time there is a sound played for some reason.

# All done!
- We are done with setting up audio splitting on Linux.
- Again, this is very dependent on your hardware and setup and this is highly untested. If you get any issues while setting this up, post an issue [here](https://github.com/sathya-pramodh/linux-mcsr/issues).
- You can go [here](https://github.com/sathya-pramodh/linux-mcsr/blob/main/doc/post-install.md#update-cycle) to continue with the post install instructions.
