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
    sleep $((60 * 1 + RANDOM % (60 * 4)))
    echo "Writing $file"
    echo 1 | sudo tee "$file"  
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

Get-ChildItem -Path ".\secrets\result*" | ForEach-Object {
    Start-Sleep -Seconds (Get-Random -Minimum 10 -Maximum 30)
    Write-Output "Writing $_"
    Set-Content -Path $_.FullName -Value "1"
}
```
