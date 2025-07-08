##  PowerShell:  Ping command  with Timestamps

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

## Bash: Ping command  with Timestamps
```bash
#!/bin/bash

# Define the IP address or hostname to ping
target="8.8.8.8"

# Loop forever and print ping replies with timestamps
while true; do
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $(ping -c 1 $target)"
    sleep 1
done
```

## Bash: Ping with Timestamps, Filtered & Logged to File
```bash
#!/bin/bash

# Set the IP address or hostname to ping
target="8.8.8.8"

# Set the output log file path
log_file="$HOME/ping_logfile.txt"

# Loop forever and log successful ping replies with timestamps
while true; do
    reply=$(ping -c 1 $target | grep 'bytes from')
    if [ -n "$reply" ]; then
        echo "$(date '+%Y-%m-%d %H:%M:%S') - $reply" >> "$log_file"
    fi
    sleep 1
done
```


## Bash: Add Timestamps to the Logfiles 
Adds timestamp to each line in log file, useful for realtime monitoring.

```bash
#!/bin/bash

# Usage: ./log_timestamper.sh /path/to/input.log /path/to/output.log

infile="$1"
outfile="$2"

if [[ -z "$infile" || -z "$outfile" ]]; then
    echo "Usage: $0 <input_log_file> <output_log_file>"
    exit 1
fi

tail -f "$infile" | awk '{ 
    print strftime("[%Y-%m-%d %H:%M:%S]"), $0; 
    fflush(); 
}' >> "$outfile"
```

### Usage
```
chmod +x log_timestamper.sh
./log_timestamper.sh /var/log/mylogfile ~/mylogfile_with_timestamp
```
