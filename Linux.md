# Commands
## ssh
TODO: link to WSL key 

```bash
sudo service ssh restart
sudo service ssh start
sudo service ssh status
```

## Save shell history
Append the new history lines to the history file. These are history lines entered since the beginning of the current Bash session, but not already appended to the history file.
```bash
history -a
```

Added to .bash_history on 23.08 02:09
```bash
shopt -s histappend
PROMPT_COMMAND="history -a;$PROMPT_COMMAND"
```

# Environment variables
Two types: shell and environment.

Show all 

# Processes
Display information of processes:
1. UNIX options, which may be grouped and must be preceded by a dash.
2. BSD options, which may be grouped and must not be used with a dash.
3. GNU long options, which are preceded by two dashes.
```bash
ps aux
pstree -p
```

# Sessions
`Session` usually refers to shell sessions. A [shell](http://en.wikipedia.org/wiki/Shell_%28computing%29) is what allows you to interact with the computer. It acts as a bridge qbetween the user and the [kernel](http://en.wikipedia.org/wiki/Kernel_%28computing%29). Whenever you run a command, it is the shell that captures your intent and tells the kernel to do its thing.

In most Linux flavors, the default shell is `bash` and a new `bash` session will be launched every time you open a new terminal.

```bash
pstree -aps
```

# Notepad++ Kubuntu
getting help
```bash
man command
command -h
which program # Executed against a program name, it will show the full path for the program.
```

if there are spaces in path: use "" or escape with \

```bash
systemctl status open-vm-tools.service
sudo apt install open-vm-tools-desktop open-vm-tools

sudo apt-get remove open-vm-tools
sudo apt-get purge open-vm-tools

sudo apt update && sudo apt upgrade

sudo service ssh restart
sudo service ssh start
sudo service ssh status

sudo apt install ubuntu-restricted-extras

/usr/bin/vmhgfs-fuse .host:/SharedFolder /home/willem-kubuntu/SharedFolder -o subtype=vmhgfs-fuse,allow_other
umount /home/willem-kubuntu/SharedFolder -v

ifconfig

apt list --installed | wc -l

lsusb

glmark2

sudo apt purge snapd && sudo apt-mark hold snapd && sudo apt autoremove && sudo apt install plasma-discover-backend-flatpak

apt list | grep nvidia

mv ~/Downloads/P3X-OneNote-2022.4.127.AppImage $HOME/opt/
chmod +x $HOME/opt/P3X-OneNote-2022.4.127.AppImage
$HOME/opt/P3X-OneNote-2022.4.127.AppImage &

timedatectl set-local-rtc 1
timedatectl

xrandr --output HDMI-0 --scale-from 2560x1440
glxinfo | grep NVIDIA

510.47

xrandr --output DP-4 --brightness
```

# Terminal commands

```bash
sudo vmware-config-tools.pl

systemctl status open-vm-tools.service
apt install open-vm-tools-desktop open-vm-tools

sudo apt-get remove open-vm-tools
sudo apt-get purge open-vm-tools

sudo apt-get install open-vm-tools
sudo apt-get install open-vm-tools-desktop

sudo service ssh restart
sudo service ssh start
sudo service ssh status

apt list --installed | wc -l

sudo apt install ubuntu-restricted-extras

ifconfig

lsusb

glxinfo -B
echo $XDG_SESSION_TYPE
export MESA_GL_VERSION_OVERRIDE=4.1
glmark2

ign gazebo shapes.sdf
```