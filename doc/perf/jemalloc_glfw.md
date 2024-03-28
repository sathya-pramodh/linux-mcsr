## Jemalloc setup for better Minecraft Performance

- To install `jemalloc` on Fedora as guided [here](https://github.com/tesselslate/resetti/blob/main/doc/troubleshooting.md#improving-malloc-performance), open up a terminal and type in the command `sudo dnf install jemalloc-devel` and type in the password as prompted.
- This should setup jemalloc for you. Just make sure to add the wrapper commands as guided in resetti's docs.

## GLFW Setup to prevent BadWindow crashes.

- To install `glfw` for Fedora as guided [here](https://github.com/tesselslate/resetti/blob/main/doc/common-issues.md#building-glfw-from-source), open up a terminal and type in the command `sudo dnf install glfw-devel` and type in the password as prompted.
- This should setup glfw for you. Using system installation of glfw for each Minecraft instance in MultiMC by going into `Edit Instance` -> `Settings` -> `Workarounds` -> `Use system installation of GLFW`
- Or you can compile and build GLFW from source and follow the instructions [here](https://github.com/tesselslate/resetti/blob/main/doc/common-issues.md#building-glfw-from-source).
