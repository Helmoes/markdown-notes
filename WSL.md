## To install
- [ ] neofetch
- [ ] starship
- [ ] powerline for bash
- [ ] upgrade ubuntu to 22.04 **after backup**!!! `sudo do-release-upgrade -d`
- [ ] `sudo apt install -y bat`
- [ ] 

In PowerShell:
```powershell
wsl -l -v
wsl --shutdown

wsl --update
```

While WSL can be disposable, it's also a good idea to back up your installations so if you do get rid of one you can get back to where you were a little easier.

Backing up is a pretty straightforward process that involves exporting to a .tar file. Our guides on exporting and importing Linux installs in WSL will take you through the process step by step, but the main commands you need are as follows:

```powershell
wsl --export <distro> <filename.tar>wsl --import <distro> <install location=""> <filename> </filename></install></distro></filename.tar></distro>
```


```powershell
wsl --export Ubuntu_20_04 C:\WSL2-Distros\backups\Ubuntu_20_04_2022(INSERT DATE!!!).tar
```

```bash
wslpath "C:\Program Files (x86)\Notepad++\notepad++.exe"
```

## Cascadia Code versions

There are multiple versions of Cascadia Code available that include ligatures and glyphs. All versions of Cascadia Code can be downloaded from the [Cascadia Code GitHub releases page](https://github.com/microsoft/cascadia-code/releases). Windows Terminal ships Cascadia Code and Cascadia Mono in its package and uses Cascadia Mono by default.

| Font Name        | Includes Ligatures | Includes Powerline Glyphs |
| ---------------- | ------------------ | ------------------------- |
| Cascadia Code    | Yes                | No                        |
| Cascadia Mono    | No                 | No                        |
| Cascadia Code PL | Yes                | Yes                       |
| Cascadia Mono PL | No                 | Yes                       |


## [](https://docs.microsoft.com/en-us/windows/terminal/cascadia-code#powerline-and-programming-ligatures)Powerline and programming ligatures

Powerline is a common command-line plugin that allows you to display additional information in your prompt. It uses a few additional glyphs to display this information properly.

Programming ligatures are glyphs that are created by combining characters. They are most useful when writing code. The "Code" variants include ligatures, whereas the "Mono" variants exclude them.