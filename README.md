# scratchpad
Notes and tidbits



#### Crt.sh Subdomain Scan 
```bash
curl -s https://crt.sh/\?q\=\%.domain.com\&output\=json | jq -r '.[].name_value' | sed 's/\*\.//g' | sort -u | httprobe | tee -a ./alive.txt
```
```powershell
(Invoke-WebRequest "https://crt.sh/?q=google.com&output=json").Content | ConvertFrom-Json -Verbose | Select-Object common_name | Get-Unique -AsString | Sort-Object | OutFile ./domains.txt
```
