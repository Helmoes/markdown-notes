# To learn
- [ ] bash 
    - [ ] environment
    - [ ] variables
    - [ ] echo
    - [ ] $
- [x] help 
- [ ] grep
- [x] less
- [x] more
- [x] cat
- [ ] nano
- [ ] awk

# getting help
```bash
man command
command -h
help command
whatis command # very short description

which program # Executed against a program name, it will show the full path for the program.

whereis gcc
whereis gdb
```

# Useful commands
## Aliases
```bash
alias ll='ls -alF'
```

## wildcards in commands (glob, globbing)
- `*`: all single characters or any string.
- `?`: one character
- `[]`: any character within the brackets
- `[!chars]`: anything except characters inside brackets

## `cat` & `bat`
The cat command, short for concatenate, not only displays file contents but can combine multiple files and show you the output of them. It’s not great for viewing large files and it’s only meant for short content.
```bash
cat foo.txt
```
### `bat` installation
```bash
wget https://github.com/sharkdp/bat/releases/download/v0.22.1/bat_0.22.1_amd64.deb
sudo dpkg -i bat_0.22.1_amd64.deb
bat --generate-config-file
```

## `less`, `more`
Use `less,` not `more`. 
Type `h` for keybindings.
- `d`: half page down
- `u`: half page up
- `g`: to beginning of file
- `G`: to end of file

## Downloading from internet with `wget`
```bash
wget https://github.com/sharkdp/bat/releases/download/v0.22.1/bat_0.22.1_amd64.deb
```

## Links to man pages
- [cp](https://manpages.ubuntu.com/manpages/jammy/en/man1/cp.1.html): `-i`, `-r`
- [mkdir](https://manpages.ubuntu.com/manpages/jammy/en/man1/mkdir.1.html)
- [mv](https://tldr.ostera.io/mv)
- [rm](https://tldr.ostera.io/rm), use with `-r` on directory to delete everything inside too
- [rmdir](https://www.gnu.org/software/coreutils/manual/html_node/rmdir-invocation.html#rmdir-invocation): only for empty directories
- 
# What is a shell?

# Packages 
Use Muon not Synaptic.
```bash
sudo apt update && sudo apt upgrade
sudo apt install firefox --install-suggests
sudo apt install ubuntu-restricted-extras
# number of packages installed:
apt list --installed | wc -l

sudo tail --lines 100 /var/log/dpkg.log | grep installed

# install .deb package
sudo dpkg -i <filename.deb>
```

# SSH server
TODO: link to WSL key 

```bash
sudo apt update && sudo apt install openssh-server

sudo systemctl status sshd
sudo systemctl start sshd
sudo systemctl enable sshd
sudo systemctl list-units -t service

ping -v -c 5 192.168.0.14

/etc/ssh/sshd_config

ssh-keygen -t ed25519

ssh-keygen -t ed25519 -o -a 100 -C "willemkuvm"
ssh-keygen -t rsa -b 4096 -o -a 100

ssh-keygen 
    -E <sha256/MD5>
# Show fingerprint of specified public key file. For RSA and DSA keys ssh-keygen tries to find the matching public key file and prints its fingerprint. If combined with -v, a visual ASCII art representation of the key is supplied with the fingerprint.
    -l
    -f <filename> # Specifies the filename of the key file.
```

- ssh is the SSH client component that runs on the user's local system
- sshd is the SSH server component that must be running on the system being managed remotely
- ssh-keygen generates, manages and converts authentication keys for SSH
- ssh-agent stores private keys used for public key authentication
- ssh-keyscan aids in collecting the public SSH host keys from hosts
- sftp is the service that provides the Secure File Transfer Protocol, and runs over SSH
- scp is a file copy utility that runs on SSH

# Save shell history
Append the new history lines to the history file. These are history lines entered since the beginning of the current Bash session, but not already appended to the history file.
```bash
history -a
```

Added to .bash_history on 23.08 02:09 
```bash
shopt -s histappend
PROMPT_COMMAND="history -a;$PROMPT_COMMAND"
```

## bash save history without exit
[source](https://superuser.com/questions/555310/bash-save-history-without-exit)
**Bash History**
Any new commands that have been issued in the active terminal can be appended to the `.bash_history` file with the following command:
```bash
history -a
```
The only tricky concept to understand is that each terminal has its own bash history **list** (loaded from the `.bash_history` file when you open the terminal)
If you want to pull any new history that's been written by other terminals during the lifetime of this active terminal, you can append the contents of the `.bash_history` **file** to the active bash history **list** 
```bash
history -c;history -r
```
This will clear the current history list so we don't get a repeated list, and append the history file to the (now empty) list.

**Solution**
You can use the bash variable `PROMPT_COMMAND` to issue a command with each new prompt (every time you press enter in the terminal)
```bash
export PROMPT_COMMAND='history -a'
```
This will record each command to the history **file** as it is issued.

**Result**
Now any new terminal you open will have the history of other terminals without having to `exit` those other terminals. This is my preferred workflow.

**More Precision**
Let's say (for some reason) you have two terminals that you're using simultaneously and you want the history to reflect between both for each new command.
```bash
export PROMPT_COMMAND='history -a;history -c;history -r'
```
The main drawback here is that you may need to press enter to re-run the PROMPT_COMMAND in order to get the latest history from the opposite terminal.
You can see why this more precise option is probably overkill, but it works for that use case.

# Bash startup
Shells may be used interactively or non-interactively. In interactive mode, they accept input typed from the keyboard. When executing non-interactively, shells execute commands read from a file.

When Bash is invoked as an interactive login shell, or as a non-interactive shell with the --login option, it first reads and executes commands from the file /etc/profile, if that file exists. After reading that file, it looks for ~/.bash_profile, ~/.bash_login, and ~/.profile, in that order, and reads and executes commands from the first one that exists and is readable. The --noprofile option may be used when the shell is started to inhibit this behavior.

When an interactive login shell exits, or a non-interactive login shell executes the `exit` builtin command, Bash reads and executes commands from the file ~/.bash_logout, if it exists. 

So: /etc/profile → ~/.bash profile → ~/.bash login → ~/.profile
>source https://devdocs.io/bash/bash-startup-files

To add directories to your PATH or define additional environment variables, place those changes in `.bash_profile` (Ubuntu uses `.profile).` For everything else, place the changes in `.bashrc`.

# File system
- /bin, /usr/bin: contains basic programs (binaries) like cat, ls, awk, etc. These two directories contain most of the programs for the system. The /bin directory has the essential programs that the system requires to operate, while /usr/bin contains applications for the system's users.
- /boot: contains files necessary to boot the system and contains kernel.
- /etc: contains critical system configuration files.
    - /etc/init.d: This directory contains the scripts that start various system services at boot time.
- /home: contains users' directories EXCEPT one special user.
- /lib: contains system libraries.
- /opt: contains optional installations.
- /proc: directory is a virtual directory, allowing direct interaction with the running Linux Kernel.
- /root: is the home directory of the specialuser called root.
- /sbin, /usr/sbin: The sbin directories contain programs for system administration, mostly for use by the superuser.
- /tmp: contains temporary files.
- /usr: contains programs like Firefox, VLC, LibreOffice, games. contains a variety of things that support user applications.
    - /usr/local: and its subdirectories are used for the installation of software and other files for use on the local machine. What this really means is that software that is not part of the official distribution (which usually goes in /usr/bin) goes here.When you find interesting programs to install on your system, they should be installed in one of the /usr/local directories. Most often, the directory of choice is /usr/local/bin.
- /var: contains system logs and runtime files.

From <[https://www.dedoimedo.com/computers/ultimate-linux-guide-for-windows-users.html#mozTocId215946](https://www.dedoimedo.com/computers/ultimate-linux-guide-for-windows-users.html#mozTocId215946)>

1: User commands; man-pages includes a small number of Section 1 pages that document programs supplied by the GNU C library. 
2: System calls documents the system calls provided by the Linux kernel. 
3: Library functions documents the functions provided by the standard C library. 
4: Devices documents details of various devices, most of which reside in /dev. 
5: Files describes various file formats and filesystems, and includes proc(5), which documents the /procfile system. 
7: Overviews, conventions, and miscellaneous. 
8: Superuser and system administration commands; man-pages includes a small number of Section 8 pages that document programs supplied by the GNU C library. 

From <https://www.kernel.org/doc/man-pages/> 

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
pstree -aps
htop
```

# Sessions
`Session` usually refers to shell sessions. A [shell](http://en.wikipedia.org/wiki/Shell_%28computing%29) is what allows you to interact with the computer. It acts as a bridge between the user and the [kernel](http://en.wikipedia.org/wiki/Kernel_%28computing%29). Whenever you run a command, it is the shell that captures your intent and tells the kernel to do its thing.

In most Linux flavors, the default shell is `bash` and a new `bash` session will be launched every time you open a new terminal.

## tmux
```bash
# start tmux
tmux
# start tmux and name session
tmux new -s my_session
# attach to running session
tmux attach-session -t my_session
```

# WSL setup
Installing gcc-11 [source](https://www.cyberciti.biz/faq/debian-ubuntu-linux-find-package-installed-updated-date/)
```bash
sudo add-apt-repository ppa:ubuntu-toolchain-r/ppa
sudo apt-get install gcc-11 --install-suggests
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-11 60
sudo apt purge snapd && sudo apt-mark hold snapd
sudo apt autoremove
```

# Kubuntu
## Drivers
[Ubuntu Manpage: lspci - list all PCI devices](https://manpages.ubuntu.com/manpages/jammy/en/man8/lspci.8.html)
`lspci` is a utility for displaying information about PCI buses in the system and devices connected to them.
By default, it shows a brief list of devices. Use the options described below to request either a more verbose output or output intended for parsing by other programs.

Options:
```bash
lspci
# Show a tree-like diagram containing all buses, bridges, devices and connections between them.
-t 
# Show kernel drivers handling each device and also kernel modules capable of handling it. Turned on by default when -v is given in the normal mode of output. (Currently works only on Linux with kernel 2.6 or newer.)
-k
```

`dmesg` 

`lsmod` - Show the status of modules in the Linux Kernel. nicely formats the contents of the /proc/modules, showing what kernel modules are currently loaded.

Driver modules dir: `/lib/modules/5.15.0-48-generic/`

## Backing up
- Timeshift for root
- Backup for home

Live USB:
- Ventoy
- Rescuezilla
- 

**24/9/22**
update grub:
```bash
sudo update-grub
```


if there are spaces in path: use "" or escape with \

```bash
ifconfig
ip a

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

## Keyboard mapping
Change file at `/usr/share/X11/xkb/symbols/pc` for shift lock to enter key.

# Gazebo
```bash
glxinfo -B
echo $XDG_SESSION_TYPE
export MESA_GL_VERSION_OVERRIDE=4.1
glmark2

ign gazebo shapes.sdf
```

# VM
```bash
sudo systemctl stop sddm.service
```