# resetti
## Using SeedQueue with resetti
- This is the Single Instance Macro we would be using to run alongside [SeedQueue](https://github.com/kingcontaria/seedqueue). This would mainly be used to configure and manage your alternate resolutions and write your own custom hooks for each of those resolutions. You can refer to SeedQueue's setup video [here](https://www.youtube.com/watch?v=fGu2MYZxh_c).
- Go to [this](https://github.com/tesselslate/resetti/releases/latest) link and download resetti's latest version.
- You can use the `.rpm` file to download the binary through rpm or you can download the binary directly. **NOTE** With the RPM download, you'll be able to execute `resetti` directly in your terminal without needing the `./` in front of it. With the binary download, you'd have to change your current directory to the directory containing the downloaded binary and then use `./resetti` to run resetti. You'd also have to set the executable flag on the binary by running `chmod +x ./resetti` in a terminal for the first time after you download the binary.
- You can check if resetti is installed correctly by running `resetti version` in a terminal and seeing if it posts, into the terminal, the version of resetti that you installed from the github.
- An example config can be found at `~/.local/share/resetti/default.toml` or `/usr/share/resetti/default.toml` depending on how you installed it.
- You can create a new profile from this example config running `./resetti new <profile_name>` in a terminal, by replacing the `<profile_name>` with whatever profile name you'd want to give.
  Eg: `./resetti new seedqueue1`
- The hooks and their documentation can be found [here](https://github.com/tesselslate/resetti/blob/main/doc/configuration.md)
- You can now run resetti with `./resetti <profile_name>` in a terminal to run the macro :D.

## Using classic wall with resetti
- If you would like to run resetti with its Wall features still, you can look [here](https://github.com/tesselslate/resetti/releases/tag/v0.6.1) to download the binary for the last stable wall release of resetti.
- After downloading, do the same steps as listed in the 3rd, 4th, 5th and 6th points under `Using SeedQueue with resetti` above.
- You can run the macro now same as above using `./resetti <profile_name>` in a terminal.
- You would need to configure everything the same way as before but you'd have to take a lot of extra steps as listed clearly [here](https://github.com/tesselslate/resetti/blob/main/doc/README.md).


If you have any questions, feel free to join the [resetti discord](https://discord.gg/fwZA2VJh7k) and make a thread in the `help` channel there.
