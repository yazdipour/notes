# Powershell

## Processes

```powershell
Start-Job -Name PrName -ScriptBlock {ls . -Recurse} // Build Bg Process
Get-Job | Stop-Job // Get & Stop (not remove) all Bg Processes
Get-Job | Remove-Job // Remove Processes in Queue
Get-Job -Name PrName | ...
Receive-Job -Name PrName  // fg Process
```