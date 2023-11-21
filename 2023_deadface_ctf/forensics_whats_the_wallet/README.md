# What's the Wallet (forensics)

## Introduction

<p align="left">
  <img height=700 img src=./readme_assets/wallet-challenge.PNG/>
</p>

> Ransomware was recently discovered on a system within De Monne’s network courtesy of a DEADFACE member. Luckily, they were able to restore from backups. You have been tasked with finding the Bitcoin wallet address from the provided sample so that it can be reported to the authorities. Locate the wallet address in the code sample and submit the flag as flag{wallet_address}.

You are given a text file.

```
# Get the current date and time
$currentTime = Get-Date

# Format the current date and time
$formattedTime = $currentTime.ToString("dddd, MMMM d, yyyy - HH:mm:ss")

# Get the current time in different time zones
$utcTime = Get-Date -Format "HH:mm:ss" -Utc
$nyTime = (Get-Date).ToUniversalTime().AddHours(-4).ToString("HH:mm:ss")
$tokyoTime = (Get-Date).ToUniversalTime().AddHours(9).ToString("HH:mm:ss")

# Display the current date and time
Write-Host "Current Date and Time: $formattedTime"
Write-Host "-----------------------------------------"

# Display the current time in different time zones
Write-Host "Current Time (UTC): $utcTime"
Write-Host "Current Time (New York): $nyTime"
Write-Host "Current Time (Tokyo): $tokyoTime"

$encrypt = "djkulwiflwingsaili2ik7h5l2bn"  

$encodedString = [System.Convert]::ToBase64String([System.Text.Encoding]::UTF8.GetBytes($encrypt))

Write-Host "Encoded String: $encodedString"

# Check if the system supports virtualization
$virtualizationEnabled = Get-WmiObject Win32_ComputerSystem | Select-Object -ExpandProperty VirtualizationFirmwareEnabled

if ($virtualizationEnabled -eq $true) {
    Write-Host "Virtualization is enabled on this system."
} else {
    Write-Host "Virtualization is not enabled on this system."
}

# Check if Hyper-V is installed and enabled
$hyperVEnabled = Get-WindowsOptionalFeature -FeatureName Microsoft-Hyper-V-All -Online | Where-Object { $_.State -eq "Enabled" }

if ($hyperVEnabled) {
    Write-Host "Hyper-V is installed and enabled on this system."
} else {
    Write-Host "Hyper-V is not installed or enabled on this system."
}

$encodedScript = @"
function Store-BtcWalletAddress {
    `$global:BtcWalletAddress = [System.Convert]::FromBase64String([System.Text.Encoding]::UTF8.GetBytes('bjMzaGE1bm96aXhlNnJyZzcxa2d3eWlubWt1c3gy'))
}

# Call the function to store the encoded Bitcoin wallet address
Store-BtcWalletAddress

# Access the stored encoded Bitcoin wallet address
Write-Host "Encoded Bitcoin Wallet Address: `$BtcWalletAddress"
"@

$encodedScriptBytes = [System.Text.Encoding]::Unicode.GetBytes($encodedScript)
$encodedScriptBase64 = [System.Convert]::ToBase64String($encodedScriptBytes)

Write-Host "Encoded Script:"
Write-Host $encodedScriptBase64

$address = "127.0.0.1"  

# Set ping parameters
$pingCount = 4
$timeout = 1000  # Timeout value in milliseconds

# Perform the ping
$pingResult = Test-Connection -ComputerName $address -Count $pingCount -TimeoutMilliseconds $timeout

if ($pingResult) {
    Write-Host "Ping to $address was successful."
    Write-Host "Ping statistics for $address:"
    Write-Host "------------------------------------"
    Write-Host "Packets: Sent = $($pingResult.Count), Received = $($pingResult.ReceivedCount), Lost = $($pingResult.Loss)"
    Write-Host "Approximate round trip times in milliseconds:"
    $pingResult | ForEach-Object {
        Write-Host "    Response from $($_.Address): time=$($_.ResponseTime)ms TTL=$($_.TimeToLive)"
    }
} else {
    Write-Host "Ping to $address failed."
}

$apiUrl = "https://api.coingecko.com/api/v3/simple/price?ids=bitcoin&vs_currencies=usd"
$response = Invoke-RestMethod -Uri $apiUrl
$bitcoinPrice = $response.bitcoin.usd
Write-Host "Current Bitcoin Price (USD): $bitcoinPrice"

$word = "Your data"
$encryptionKey = "MyEncryptionKey123" 

$secureString = ConvertTo-SecureString -String $word -AsPlainText -Force
$encryptedData = ConvertFrom-SecureString -SecureString $secureString -Key (1..16 | ForEach-Object { $encryptionKey[$_] })
$encryptedString = [System.Text.Encoding]::UTF8.GetString($encryptedData)

Write-Host "Encrypted Word: $encryptedString"

$message = "Y0ur D@tA has been 3ncrypted pay 100 BTC (Bitcoin) to Deadface"
```

## Solution

Download the attached txt file and search for the wallet address. It is base64 encoded. 

Decode from base64 using [CyberChef](https://gchq.github.io/CyberChef/) to get the flag.

## Flag

**`flag{n33ha5nozixe6rrg71kgwyinmkusx2}`**

## Tools

- [CyberChef](https://gchq.github.io/CyberChef/)



