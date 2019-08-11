# Powershell

## Processes

```powershell
Start-Job -Name PrName -ScriptBlock {ls . -Recurse} // Build Bg Process
Get-Job | Stop-Job // Get & Stop (not remove) all Bg Processes
Get-Job | Remove-Job // Remove Processes in Queue
Get-Job -Name PrName | ...
Receive-Job -Name PrName  // fg Process
```

## Remove (Preinstalled) Applications

`Get-AppxPackage *bingweather* | Remove-AppxPackage`

## To install Net35

`Dism.exe /online /enable-feature /featurename:NetFX3 /All /Source:c:\sxs /LimitAccess`

## Some Commands

|What|Command|
|-|-|
| Make a setup  | `iexpress`
| To repair windows files | `sfc /scanner`
| Check wifi drive  | `netsh wlan show drivers` (check HOTSPOT NET SUPPORT)
| Show Wifis info | `netsh wlan show networks`
| Change IP and default gateway:  | `netsh int ip set address "local area connection" static 192.168.0.101 255.255.255.0 192.168.0.254 1`
| Change DNS:  | `netsh int ip set dns "local area connection" static 192.168.0.254 primary`
| Hide directory | `attrib +s +h targetdir`
| Install Appx | `Add-appxpackage dir`
| Restart Store | `wsreset`
| To extract exe file | `setup.exe /e extract`
| To active Admin user | `net user administrator <pass> /active:yes`
| Change User Password | `net user %targetuser% %urpassword%`
