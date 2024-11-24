## Jemalloc setup for better Minecraft Performance

- To install `jemalloc` on Fedora as guided [here](https://github.com/tesselslate/resetti/blob/main/doc/optimization.md#malloc-improvements), open up a terminal and type in the command `sudo dnf install jemalloc-devel` and type in the password as prompted.
- This should setup jemalloc for you. Just make sure to add the wrapper commands as guided in resetti's docs.

## GLFW Setup to prevent BadWindow crashes.

- To prevent GLFW's BadWindow crashes when you tab out of an instance of Minecraft, you can go into your launcher settings and look for the version of LWJGL. If the version is 3.2.2, we strongly recommend upgrading to a higher version like 3.3.3.
- If not, you can also use a system installation of GLFW by running the command `sudo dnf install glfw-devel` and then setting your launcher to use this GLFW shared object instead. This file exists at `/usr/lib64/libglfw.so`.

## Setup to prevent cursor warping on opening inventory.

- To prevent this we recommend using [this](https://unix.stackexchange.com/questions/491531/how-to-avoid-mouse-cursor-jumping-while-using-xinput-coordinate-transformation-m/639730#639730) formula to set your Coordinate Transformation Matrix to some value based on your cursor speed.
- You would need to look for the id for your mouse using `xinput`.
- First install `xinput` using the command `sudo dnf install xinput` in a terminal.
- Run `xinput` to see all the input devices it recognizes.
- Search for the device that has the same name as your mouse and has a `[slave pointer (n)]` on the same line as the name.
- Eg: `↳ Logitech G304                           	id=15	[slave  pointer  (2)]`
- Take this id and this is the id that you would use to get your Coordinate Transformation Matrix as listed in the stackexchange thread.
- Eg: The id for my mouse from the above example is `15`.
- After applying the matrix to your mouse, make sure to execute it on startup with an entry into `~/.config/autostart` or into your window manager's config file/startup script.
- **NOTE** For i3 users, you can put `exec --no-startup-id <xinput_command>` into `~/.config/i3/config` so that it works across reboots.
- Eg: Since I use a cursor speed of `0.125` and want my mouse to always spawn at `960, 540` on my screen, on applying the formula, I get the Transformation Matrix as `0.125 0 840 0 0.125 472.5 0 0 1`. So I would put `exec --no-startup-id xinput set-prop 15 "Coordinate Transformation Matrix" 0.125 0 840 0 0.125 472.5 0 0 1` into my i3 config.
