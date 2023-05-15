# Linux Terminal
In this document, we will be learning the basics of the Linux Terminal. We will go through all the basic commands with examples for each.

# What is a terminal?
- It's a part of every system (irrespective of Operating System) that helps you control the system from a very stripped down level (without a Graphical User Interface). Programs or Commands can be run from here to perform some task on the system.
- It is a very powerful tool and most of the time, GUI applications have these commands running in the back when you click buttons to perform actions.
- You can open up a terminal on Linux Mint by hitting the keybind `Ctrl+Shift+T`.

# Directories
- A directory is like a folder on your computer under which files or other folders can exist.
- In Linux, everything on your system, including the hardware devices that you have connected to your computer will be available for use as a file. It's a UNIX system convention.
- The `/` directory in your system is the root of your file system. It has everything that is on your storage that is mounted.
- [Here](https://www.howtogeek.com/117435/htg-explains-the-linux-directory-structure-explained/) are some of the directories in `/` and description of what they hold.
- In the terminal type in this command 
```bash
cd Desktop
```
- The `cd` command is used to change your current working directory (the current folder that you have open) to the directory that you specify. `Desktop` in this case.
- There are some shortcut characters that you can use to make your life easier while working with directories.
- The symbol `~` is used to refer to the user's home folder (`/home/<user_name>`).
```bash
cd 
```
- Now type
```bash
ls
```
- The `ls` command is used to list out the contents of your current directory.
- You can use some flags to tell the command what to output.
- Type in
```bash
ls -l
```
- The `-l` flag can be used to long list (or vertical list) out the contents along with the permissions on each file/folder.
- Now type
```bash
ls -a
```
- The `-a` flag can used to show all files and folders in the current directory along with the hidden files.
- You can use both of the above commands in unison like this
```bash
ls -la
```
- You can make directories inside your current directory using the `mkdir` command.
```
mkdir test
```
- If you want to create multiple directories inside of each other, then we use the `-p` flag.
```
mkdir -p test1/test11
```
- This would create a `test1` directory in your current directory and create a `test11` directory inside of `test1`.
- If you want to remove all these directories that you created just now, you can use either `rmdir` or `rm`.
- `rmdir` is used to delete directories that are empty.
```
rmdir test
```
- This would work because `test` is empty. But the same thing wouldn't work with `test1` as it has a `test11` directory inside it.
- So we use the `rm` command with the `-r` flag to remove it.
```
rm -r test1
```
- The `-r` flag represents recursive removal. You can also use the `-f` flag to force remove the directories.
- Remember, `-f` would remove everything even if it is read-only.
- You can create a new file using the `touch` command.
```
touch text.txt
```
- You can view the contents of this file by using the `cat` command.
```
cat text.txt
```
- This wouldn't output anything as the file is empty. You can open this file right in the terminal by using `nano` which is a terminal based editor.
```
nano text.txt
```
- Once you are done editing the contents you can hit `Ctrl+S` and `Ctrl+X` to save and quit.
- You can remove this file now with `rm`.
```
rm text.txt
```

# Super User Privileges
- Super user privileges are admin privileges or elevated privileges given to a user in any UNIX system.
- To execute commands as a super user, we use the `su` command. `su` stands for switch user.
- Try executing
```bash
su -
```
- Now a terminal would open with a different color to denote that you have super user privileges. In this terminal, you literally can nuke your whole system. So be careful about what you do in here.
- To get back to your normal user terminal, type
```bash
exit
```
- If you want to execute only some commands with super user privileges, you can use the wrapper command `sudo`.
- This is safer as you can be sure to execute each command with the right permissions.
- Try out this command
```bash
sudo apt update
```
- Super user privileges are required for package manager commands on any Linux system.
- So to install packages you will be prompted to give your password.
- While typing in the password, the terminal would not respond with a `*` being filled in place of the characters in other distributions. But Linux Mint has a default setting to show a `*` for every character.

# Pipe
- The Pipe symbol (`|`) is used to chain the outputs of certain commands into other commands.
- There are several uses to this symbol, but the most common usage is to use it alongside the `grep` command.
- Try this command
```bash
touch text.txt
ls | grep text.txt
```
- `grep` is used to print out all the lines within an output or a file with `text.txt` in it.
- You can pipe the output of any command into `grep` and get the matching lines based on your search term.

# File permissions
- File permissions in a UNIX system are distributed per user.
- The only permission we really care about is the executable flag.
- This flag tells the operating system that it can execute that file as a binary.
- To set the executable flag on a file we use the `chmod` command.
```bash
touch bin
chmod +x bin
```
- Now edit the contents of `bin` with 
```bash
nano bin
```
- Add these contents in it
```bash
#!/bin/bash
echo "Hello World"
```
- Here the echo command is used to print out text to the console.
- To execute this script, we use this command 
```bash
./bin
```
- You would see the console output `Hello World`.
- There are other permissions too, but we mostly use `chmod +x` to set the executable flag on files.
- We can also remove the executable flag from a file by using `chmod -x`.
```
chmod -x bin
```

# Clearing out worlds
- Now that we know much about the Linux terminal, we can now make scripts to automate our filesystem tasks.
- We can declare variables in scripts using the syntax:
```bash
<variable_name>=<value>
```
- Here is a script to clear out saves in all your instances.
```bash
#!/bin/bash
instance_prefix="Speedrun"
instance_num=12
# DO NOT add a '/' at the end of mmc_prefix's value
mmc_prefix=~/.local/share/multimc/instances
for i in $(seq 1 $instance_num);
do
    rm -r $mmc_prefix/$instance_prefix$i/saves/Random*
done
```
- Here in the `rm` command, we actually use a shorthand representation to expand every folder starting with `Random` in its name. So its matches would look something like `Random Speedrun #12345`, `Random Speedrun #12346` and so on
- We also use the `seq` command which gives us a range which can be iterated over for example in a for loop. You can test it by trying out `seq 1 12` in a terminal.
- We also use a for loop in bash to loop over every instance number and delete every world folder.

# Launch all instances
- We can launch all our instances by using a script too!
- Here is one to launch all instances of a particular format.
```bash
#!/bin/bash
instance_prefix="Speedrun"
instance_num=12
mmc_binary=multimc
for i in $(seq 1 $instance_num);
do
    $mmc_binary -l $instance_prefix$i &
done
```
- The `multimc` binary has a flag `-l` which you can pass to launch that instance.
- We also use the `seq` command which gives us a range which can be iterated over for example in a for loop. You can test it by trying out `seq 1 12` in a terminal.
- Here we also use an `&` at the end of the command to background the process. This is done so that all instances launch together.
- The profile for the instance would be the default profile as we are not specifying it during launch.

# Going ahead
- We are now proficient with the Linux terminal and bash scripting.
- Congratulations! Now you can proceed back to the post install setup [here](https://github.com/sathya-pramodh/linux-mcsr/blob/main/doc/post-install.md#nvidia-drivers).
