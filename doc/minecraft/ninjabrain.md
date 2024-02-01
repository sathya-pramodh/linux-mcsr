# NinjabrainBot

- Download the .jar for NinjabrainBot as per usual from [here](https://github.com/Ninjabrain1/Ninjabrain-Bot/releases/latest).
- Lets take an example where the .jar file is downloaded into the **Downloads** folder.
- Now to add it as an application to your list of applications, create this file with the following contents under `~/.local/share/applications/NinjabrainBot.desktop`

```bash
[Desktop Entry]
Encoding=UTF-8
Type=Application
Name=NinjabrainBot
Icon=minecraft
Exec=java -jar /home/<user_name>/Downloads/Ninjabrain-Bot-1.4.1.jar
```

- If the directory does not exist, then make the directory/directories by executing the following command in a terminal

```bash
mkdir -p ~/.local/share/applications/
```

- Remember that the file name will change over versions. So as you update Ninjabrain Bot, you will have to change this file as well. Also, you will have to replace `<user_name>` with your username that you set during the install.
- If you downloaded it elsewhere, then replace `/home/<user_name>/Downloads/Ninjabrain-Bot-1.4.1.jar` with the relevant path.
- Now you can launch Ninjabrain Bot from your applications menu!
