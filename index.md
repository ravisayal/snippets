##  PowerShell: Better Ping command  with Timestamps

``` powershell
# Define the IP address or hostname to ping
$target = "8.8.8.8"

# Loop forever and log ping replies with timestamps
while ($true) {
    "$(Get-Date -Format 'yyyy-MM-dd HH:mm:ss') - $(ping -n 1 $target )" 
    Start-Sleep -Seconds 1
}
```

##  PowerShell: Better Ping command with Timestamps, using filter and appending output to file.

``` powershell
# Set the IP address or hostname to ping
$target = "8.8.8.8"

# Set the output log file path
$logFile = "$HOME\ping_logfile.txt"

# Loop forever and log ping results with timestamps
while ($true) {
    "$(Get-Date -Format 'yyyy-MM-dd HH:mm:ss') - $(ping -n 1 $target | Select-String 'Reply from')" |
        Out-File -Append -FilePath $logFile
    Start-Sleep -Seconds 1
}
```
