
```powershell
bcdedit /set hypervisorlaunchtype off
bcdedit /set hypervisorlaunchtype auto
```

## version
```powershell
$PSVersionTable
$env:PSModulePath
$env:PSModulePath.replace(';',"`n")
```

## gets PowerShell modules that are installed on a computer using PowerShellGet
```powershell
Get-InstalledModule
```

## Without parameters, Get-Module gets modules that have been imported into the current session.
```powershell
Get-Module
Get-Command -Module vmxtoolkit
```

```powershell
Install-GuiCompletion
Get-PSReadLineOption
```

## format output
    | Format-List
    | Format-Table


```powershell
vmrun start full/path/of/your/virtual/machine/bundle nogui
```
