# Setting up tmpfs

You should get better performance while running wall by symlinking your instance world folders into `/tmp/mc/` and setting `/tmp` as a tmpfs volume.
What that means is that files in these folders will be stocked in your memory and deleted on every reboot.

- First define `/tmp` as a tmpfs volume by adding the following line to `/etc/fstab`

```bash
tmpfs /tmp tmpfs defaults,size=Xg 0 0
```

Replace X with the number of gigabits you want to allocate, it won't use all of it if not needed but this sets a limit.

- E.g. While running PrismLauncher (a fork of MultiMC), I would symlink `~/.local/share/PrismLauncher/instances/Instance1/.minecraft/saves` to `/tmp/mc/1/` and so on by using the command below for each, ensure you have deleted the `saves` folder beforehand.

```bash
ln -s  /tmp/mc/1 ~/.local/share/PrismLauncher/instances/Instance1/.minecraft/saves
```

As the `/tmp` folder is cleared on every restart you need to setup a script to create the folder on every boot, if your distribution uses `systemd` you could do something like this:

- First create the file `/etc/rc.local` with the following content :

```bash
#!/bin/bash

mkdir /tmp/mc
for i in {1..X} # Replace X with the number of instances you use
do
  mkdir /tmp/mc/$i
  #---------Optional Part if you want to import your practice maps--------
  # First you need to put all your practice maps in the same foder somewhere on your pc for me
  # it's in /home/username/Documents/speedrun/maps
  ln -s "/home/username/Documents/speedrun/maps/ZCrafting Practice v2" /tmp/mc/$i/
  ln -s "/home/username/Documents/speedrun/maps/ZLBP 3.14.0" /tmp/mc/$i/
  ln -s "/home/username/Documents/speedrun/maps/ZOW Practice V2" /tmp/mc/$i/
  ln -s "/home/username/Documents/speedrun/maps/ZPortal Practice v2" /tmp/mc/$i/
  ln -s "/home/username/Documents/speedrun/maps/ZRyguy2k4 End Practice v3.4.0-1.16.1" /tmp/mc/$i/
  # adapt the previous commands depending on your maps and their location
  #---------End Optional Part-------------
  chown username -R /tmp/mc/$i # Replace username by yours
done
```

After the file is saved, execute

```bash
sudo chmod +x /etc/rc.local
```

Then run the following commands

```bash
sudo nano /etc/systemd/system/rc-local.service
```

And enter the following content

```
[Unit]
Description=/etc/rc.local Compatibility
ConditionPathExists=/etc/rc.local

[Service]
Type=forking
ExecStart=/etc/rc.local start
TimeoutSec=0
StandardOutput=tty
RemainAfterExit=yes
SysVStartPriority=99

[Install]
WantedBy=multi-user.target
```

Now run the following commands and check that the folders created successfully

```bash
sudo systemctl enable rc-local
sudo systemctl start rc-local
```

**NOTE: If you don't have systemd on your distribution, you can use the same script and run it at the start of your session.**

- And now you can keep clearing out these folders every 300s or so by running a simple script in the background.
- This script preserves the training maps (their folder name must start with "Z") and the last 5 random worlds for verification purposes.
- Replace "X" with your number of instances.

```bash
#!/bin/bash
IFS=$'\n'
while true
do
    for i in {1..X}
    do
        for save in $(ls /tmp/mc/$i -t1 --ignore=Z* | tail -n +6)
        do
            rm -r "/tmp/mc/$i/$save"
        done
    done
    sleep 300
done
```

- Here the "X" in the for loop is the total number of instances that you have. Make sure to name the folders exactly as in the above example for this script, i.e., `/tmp/mc/1` and so on.
- Now set the executable flag on the script by performing the following command in a terminal

```bash
chmod +x script.sh
```

- And execute it everytime you start your resetting session with the following command

```bash
./script.sh
```

- **NOTE: Use this method IF AND ONLY IF you have some RAM to spare with all the instances running and resetting. DO NOT use it if you are using >70-80% of RAM during resetting as running that script in the background takes up memory as well!**
