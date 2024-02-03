# File permissions

File permissions in a UNIX system are distributed per user.

The only permission we really care about is the executable flag.
This flag tells the operating system that it can execute that file as a binary.

To set the executable flag on a file we use the `chmod` command.

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

We are now proficient with the Linux terminal and bash scripting!
