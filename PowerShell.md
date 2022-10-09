## Aliases
```powershell
wsllv -> wsl -l -v
```

New alias template:
```powershell
function cmd { cmd.exe /c $args there }
```

## Drivers
```powershell
echo $Env:Path
```

## SSH & hypervisor
https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.management/get-service?view=powershell-7.2#parameters
```powershell
Get-Service -Displayname "*ssh*"
```

```powershell
bcdedit /set hypervisorlaunchtype off
bcdedit /set hypervisorlaunchtype auto
```

## elevate .ps1 script for admin rights
```powershell
# Self-elevate the script if required

if (-Not ([Security.Principal.WindowsPrincipal] [Security.Principal.WindowsIdentity]::GetCurrent()).IsInRole([Security.Principal.WindowsBuiltInRole] 'Administrator')) {

    if ([int](Get-CimInstance -Class Win32_OperatingSystem | Select-Object -ExpandProperty BuildNumber) -ge 6000) {

        $CommandLine = "-File `"" + $MyInvocation.MyCommand.Path + "`" " + $MyInvocation.UnboundArguments

        Start-Process -FilePath pwsh.exe -Verb Runas -ArgumentList $CommandLine

        Exit

    }

}

# rest of the script
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
