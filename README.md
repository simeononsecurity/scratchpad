# scratchpad
Notes and tidbits



#### Crt.sh Subdomain Scan 
```bash
curl -s https://crt.sh/\?q\=\%.domain.com\&output\=json | jq -r '.[].name_value' | sed 's/\*\.//g' | sort -u | httprobe
```
```powershell
(Invoke-WebRequest -UseBasicParsing "https://crt.sh/?q=google.com&output=json").Content | ConvertFrom-Json -Verbose | ForEach-Object { (Write-Output ($_).common_name, ($_).name_value | Where-Object { $_ -notmatch "(.*[*].*$)|(.*[@].*)" }) } | Sort-Object | Get-Unique -AsString | Sort-Object | ForEach-Object { Set-Variable -Name domains -Value $_; ForEach ($domain in $domains) {if ((Invoke-WebRequest -Uri $domain -ErrorAction "Ignore").StatusCode -eq "200") { Write-Host $Domain } } } 
```
