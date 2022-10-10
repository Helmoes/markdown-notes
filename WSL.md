# To install
- [ ] check advanced setting (swap, gpu, ...)
- [ ] neofetch
- [ ] starship
- [ ] powerline for bash
- [ ] upgrade ubuntu to 22.04 **after backup**!!! `sudo do-release-upgrade -d`
- [ ] `sudo apt install -y bat`
- [ ] 

# In PowerShell:
```powershell
wsl -l -v
wsl --shutdown

wsl --update
```

While WSL can be disposable, it's also a good idea to back up your installations so if you do get rid of one you can get back to where you were a little easier.

Backing up is a pretty straightforward process that involves exporting to a .tar file. Our guides on exporting and importing Linux installs in WSL will take you through the process step by step, but the main commands you need are as follows:
```powershell
wsl --export Ubuntu-20-04 C:\WSL2-Distros\backups\Ubuntu_20_04_20221010.tar
```

```powershell
wsl --export <distro> <filename.tar>wsl --import <distro> <install location=""> <filename> </filename></install></distro></filename.tar></distro>
```

```bash
wslpath "C:\Program Files (x86)\Notepad++\notepad++.exe"
```
