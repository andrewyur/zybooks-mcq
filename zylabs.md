# Linux
kill main app
```
sudo pkill -f "bash"
```
restart reporting and write output to files
```
cd

bash itlabs_reporting.sh 2>/dev/null &

for file in ./secrets/result*; do
    if [$(cat $file == "0"]; then
        echo "Writing $file"
        echo 1 | sudo tee "$file"  
        sleep $((60 * 3 + RANDOM % (60 * 3)))
    fi
done
```

# Windows
kill main app
```
Get-Process -Name powershell | Where-Object {
    ($_.Path -like "*powershell.exe" -or $_.Path -like "*pwsh.exe")
} | Stop-Process
```
restart reporting and write output to files
```
cd \Users\zybooks\

Start-Process -FilePath "powershell.exe" -ArgumentList "-File C:\Users\zybooks\itlabs_reporting.ps1"

Get-ChildItem -Path ".\secrets\result*" | Where-Object {
    (Get-Content -File $_.FullName) -eq "0"
} | ForEach-Object {
    Write-Output "Writing"
    Set-Content -Path $_.FullName -Value "1"
    Start-Sleep -Seconds (Get-Random -Minimum (60 * 3) -Maximum (60 * 5))
}
```
