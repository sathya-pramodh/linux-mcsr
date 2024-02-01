## Jemalloc setup for better Minecraft Performance

- To install `jemalloc` on Linux Mint as guided [here](https://github.com/woofdoggo/resetti/blob/main/doc/troubleshooting.md#improving-malloc-performance), open up a terminal and type in the command `sudo apt install libjemalloc-dev` and type in the password as prompted.
- This should setup jemalloc for you. Just make sure to add the wrapper commands as guided in resetti's docs.

## GLFW Setup to prevent BadWindow crashes.

- To install `glfw` for Linux Mint as guided [here](https://github.com/woofdoggo/resetti/blob/main/doc/common-issues.md#building-glfw-from-source), go into the **Software Manager** and search for **glfw** and install the first package that shows up.
- This should setup glfw for you. Using system installation of glfw for each Minecraft instance in MultiMC by going into `Edit Instance` -> `Settings` -> `Workarounds` -> `Use system installation of GLFW`
- Or you can compile and build GLFW from source and follow the instructions [here](https://github.com/woofdoggo/resetti/blob/main/doc/common-issues.md#building-glfw-from-source).
