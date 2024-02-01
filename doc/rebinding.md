# Rebinding Keys (for bookcrafting)

- Install `xdotool` and `xbindkeys` from the **Software Manager** by searching for them.
- Now edit the file name `.xbindkeysrc` in your home directory (shorthanded with `~`) and add these lines inside the file to rebind the one key to the other

```
"xdotool key '<Rebound key combination>'"
    release+'<Original key combination>'
```

- E.g: If you want to rebind `r` to `6` then you would add these lines

```
"xdotool key '6'"
    release+r
```

- You can just read the examples given in the file to understand clearly how to do it for a modifier setup or for binding a combination of keys.
- Now run the following command in a terminal to background the process and bind all the keybinds set in `.xbindkeysrc`

```bash
xbindkeys
```

- If you don't want to background the xbindkeys process (useful for debugging), then execute the following command

```bash
xbindkeys -v
```

- Note that you need to do one of these above commands in a terminal before you start your resetting session.
