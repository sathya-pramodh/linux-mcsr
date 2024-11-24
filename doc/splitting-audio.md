# Splitting audio

In this document we will be setting up Virtual Audio Inputs and splitting audio outputs in OBS. Remember! This method is highly untested and it works very well on my PC at the moment. But if you have any issues, post it [here](https://github.com/sathya-pramodh/linux-mcsr/issues).

# qpwgraph

This is the app that will let us split audio easily with a GUI. You can download it by executing this in your terminal

```
sudo dnf install qpwgraph
```

We now need to setup `qpwgraph` such that it launches each time with the correct arguments on startup.  
Copy the following contents into a file named `qpwgraph.desktop` and drop it in `~/.config/autostart/`

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

We will be using this application later on to setup output routing.  

**NOTE**: If you are using a window manager, make sure to add `qpwgraph <path_to_config> -axm` to your autostart script for your window manager by replacing `<path_to_config>` with the path of the config you save later on during the setup.  
Eg: In i3, say a config is in `~/Speedrunning.qpwgraph`, then we put `exec qpwgraph ~/Speedrunning.qpwgraph -axm` in `~/.config/i3/config`.

# Setting up Virtual Audio Devices

`virtual-input-1` and `virtual-input-2` can be renamed to make things more easily identifiable for yourself. But for the purpose of this guide, I'll be using those two names.

We're going to use `.conf` files to configure virtual devices. These files should be placed in `~/.config/pipewire/pipewire.conf.d` (for user configuration) or `/etc/pipewire/pipewire.conf.d` (for system-wide configuration).

First, add a file `virtual-input-1.conf` with the following contents.
```
context.objects = [
	{	factory = adapter
		args = {
			factory.name = support.null-audio-sink
			node.name = "virtual-input-1"
			media.class = Audio/Sink
		}
	}
]
```

Next, add another file `virtual-input-2.conf` with the following contents.

```
context.objects = [
	{	factory = adapter
		args = {
			factory.name = support.null-audio-sink
			node.name = "virtual-input-2"
			media.class = Audio/Sink
		}
	}
]
```


This will create two virtual audio devices whenever pipewire service starts. If you want to have more virtual devices, you may add more to your liking. To take immediate effect, you can simply restart pipewire service with the command

```
systemctl --user daemon-reload && systemctl --user restart pipewire
```

qpwgraph should now show two nodes with the names `virtual-input-1` and `virtual-input-2`.  
Again, you can change out any instance of `virtual-input-1` and `virtual-input-2` to something else as they are just names. I just use them as it is to keep things consistent across the guide.

# Setting up OBS

Now head to OBS and make a scene called `Audio` for the sake of simplicity. Inside the scene, add two `JACK Input Client` sources called `virtual-input-1` and `virtual-input-2`. Just leave the properties as default. After adding the sources within the scene, add the scene to the scenes that you want audio in.

# Setting up Audio Splits

Open up qpwgraph and you should see the nodes `OBS Studio: virtual-input-1` and `OBS Studio: virtual-input-2`. Connect them to the virtual devices by dragging the `monitor_FL` and `monitor_FR` of `virtual-input-1` to `virtual-input-1:in_1` and `virtual-input-1:in_2` of `OBS Studio: virtual-input-1` respectively. Do the same for `OBS Studio: virtual-input-2`.

If you wanna not have your Spotify music appear on VODs, you can route Spotify into one of the virtual devices, like `virtual-input-2`, by dragging `output_FL` to `playback_FL` and `output_FR` to `playback_FR`.

Now on OBS, go into `Settings`, then to the `Output` tab. Under `Streaming`, tick the `Twitch VOD Track` box. If you're on simple output mode, it should default to 2. If you're in advanced output mode, pick 2.

Now go back to the your OBS scene and click on the gear icon under `Audio Mixer`. There, you'll deselect track number 2 of the audio that contains your Spotify music. In this case, that is `virtual-input-2`. So deselect track 2 of `virtual-input-2` and now your Spotify music will not be inside your Twitch VODs.

Similarly, route any other audio that you want into your virtual devices, i.e. your Minecraft instances or lecture videos.

Now hit `Ctrl + S` to save changes in qpwgraph.

If you have any issues regarding Spotify desktop app connections flickering from one virtual device to the other, you may post an issue [here](https://github.com/sathya-pramodh/linux-mcsr/issues).

# All done!

- We are done with setting up audio splitting on Linux.
- Again, this is very dependent on your hardware and setup and this is highly untested. If you get any issues while setting this up, post an issue [here](https://github.com/sathya-pramodh/linux-mcsr/issues) or even better, join the [resetti Discord server](https://discord.gg/g9b99fxW) and we'll try and help you.
