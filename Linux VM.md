# Commands
```bash
sudo apt-get install open-vm-tools-desktop
systemctl status open-vm-tools.service

sudo apt-get remove open-vm-tools
sudo apt-get purge open-vm-tools

glxinfo | grep direct
glxgears
glxinfo | grep OpenGL

/usr/bin/vmhgfs-fuse .host:/SharedFolder /home/willem-kubuntu/SharedFolder -o subtype=vmhgfs-fuse,allow_other
/usr/bin/vmhgfs-fuse .host:/SharedFolder /home/willem/SharedFolder -o subtype=vmhgfs-fuse,allow_other
umount /home/willem-kubuntu/SharedFolder -v
```

