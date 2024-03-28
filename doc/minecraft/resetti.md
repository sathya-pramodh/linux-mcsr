# resetti

- This is the Multi Instance macro we will be using on Linux.
- To install it, go [here](https://github.com/tesselslate/resetti/releases/tag/v0.5.2-beta). Download the binary from the github release. If you are using Firefox (the default browser for Fedora) it should download the binary to the **Downloads** folder. If you download it elsewhere, replace **Downloads** with the path to that folder in the command given below. E.g: If you download it to your **Documents** folder, then your path would look something like `/home/<user_name>/Documents`.
- To update the binary, delete the binary from your **Downloads** folder and then go through the install process for **resetti** again.
- For more detailed install instructions with setup for OBS and everything, refer to the docs for **resetti** [here](https://github.com/tesselslate/resetti).
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

- Here, replace **<config_name>** with the configuration name you want to use. All about the configuration of the macro is, again, given in the docs for **resetti** [here](https://github.com/tesselslate/resetti/).
- If you have any questions, asking it in the [resetti discord](https://discord.gg/fwZA2VJh7k) is your best option.
