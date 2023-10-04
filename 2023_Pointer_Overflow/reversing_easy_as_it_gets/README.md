# Easy as it Gets, (reversing, 129 solves, 100p)

## Introduction

<p align="left">
  <img height=700 img src=./readme_assets/easy-challenge.PNG/>
</p>

We are given a link to a **`powershell script`** file.

## Task analysis

Look at the **`powershell script`** and find the password.

## Enumeration
```
[Reflection.Assembly]::LoadWithPartialName("System.Security")  

function Encrypt-String($String, $Passphrase, $salt="SaltCrypto", $init="IV_Password", [switch]$arrayOutput)  
{  
    $r = new-Object System.Security.Cryptography.RijndaelManaged  
    $pass = [Text.Encoding]::UTF8.GetBytes($Passphrase)  
    $salt = [Text.Encoding]::UTF8.GetBytes($salt)  
    $r.Key = (new-Object Security.Cryptography.PasswordDeriveBytes $pass, $salt, "SHA1", 5).GetBytes(32) #256/8  
    $r.IV = (new-Object Security.Cryptography.SHA1Managed).ComputeHash( [Text.Encoding]::UTF8.GetBytes($init) )[0..15]  
    $c = $r.CreateEncryptor()  
    $ms = new-Object IO.MemoryStream  
    $cs = new-Object Security.Cryptography.CryptoStream $ms,$c,"Write"  
    $sw = new-Object IO.StreamWriter $cs  
    $sw.Write($String)  
    $sw.Close()  
    $cs.Close()  
    $ms.Close()  
    $r.Clear()  
    [byte[]]$result = $ms.ToArray()  
    return [Convert]::ToBase64String($result)  
}  
  
function Decrypt-String($Encrypted, $Passphrase, $salt="SaltCrypto", $init="IV_Password")  
{  
    if($Encrypted -is [string]){  
        $Encrypted = [Convert]::FromBase64String($Encrypted)  
    }  

    $r = new-Object System.Security.Cryptography.RijndaelManaged  
    $pass = [Text.Encoding]::UTF8.GetBytes($Passphrase)  
    $salt = [Text.Encoding]::UTF8.GetBytes($salt)  
    $r.Key = (new-Object Security.Cryptography.PasswordDeriveBytes $pass, $salt, "SHA1", 5).GetBytes(32) #256/8  
    $r.IV = (new-Object Security.Cryptography.SHA1Managed).ComputeHash( [Text.Encoding]::UTF8.GetBytes($init) )[0..15]  
    $d = $r.CreateDecryptor()  
    $ms = new-Object IO.MemoryStream @(,$Encrypted)  
    $cs = new-Object Security.Cryptography.CryptoStream $ms,$d,"Read"  
    $sr = new-Object IO.StreamReader $cs  

    Write-Output $sr.ReadToEnd()  

    $sr.Close()  
    $cs.Close()  
    $ms.Close()  
    $r.Clear()  
}  

cls  

#### 
# TODO: use strong password
# Canadian_Soap_Opera
### 

$pwd = read-host "(Case Sensitive) Please Enter User Password"  

$pcrypted = "TTpgx3Ve2kkHaFNfixbAJfwLqTGQdk9dkmWJ6/t0UCBH2pGyJP/XDrXpFlejfw9d"  

write-host "Encrypted Password is: $pcrypted"  
write-host ""  
write-host "Testing Decryption of Username / Password..."  
write-host ""      

$pdecrypted = Decrypt-String $pcrypted $pwd 

write-host "Decrypted Password is: $pdecrypted"  
``` 
## Solution

Looking at the code you can see the password in the comments. **`Canadian_Soap_Opera`**.

<p align="left">
  <img height=300 img src=./readme_assets/password.PNG/>
</p>

Run the code in **`VScode`** using the password and get the flag. 

<p align="left">
  <img height=300 img src=./readme_assets/decrypted.PNG/>
</p>

## Flag

**`poctf{uwsp_4d_v1c70r14m_w4573l4nd3r}`**

## Tools

- **`VScode`**

