# M Three Sixty Five (challenge-group, 507 solves, 50 points)

## Introduction

<p align="left">
  <img height=400 img src=./readme_assets/m365-challenge.PNG/>
</p>

## Solution

***M Three Sixty Five - General Info***

*Welcome to our hackable M365 tenant! Can you find any juicy details, like perhaps the street address this organization is associated with?*

Googled `aadinternals powershell` to find commands to help with the challenge. I am able to use most Linux commands but can't find anything using grep.

Using `Get-AADIntTenantDetails` you get he flag for part 1.

<p align="left">
  <img height=400 img src=./readme_assets/m3653.PNG/>
</p>

**`flag{dd7bf230fde8d4836917806aff6a6b27}`**

***M Three Sixty Five - Conditional Access***

*This tenant looks to have some odd Conditional Access Policies. Can you find a weird one?*

Using `Get-AADIntConditionalAccessPolicies` you get the flag for part 2.


**`flag{d02fd5f79caa273ea535a526562fd5f7}`**

***M Three Sixty Five - Teams***

*We observed saw some sensitive information being shared over a Microsoft Teams message! Can you track it down?*

Using `Get-AADIntTeamsMessages | Format-Table id,content,deletiontime,*type*,DisplayName` we get the flag for part 3.

<p align="left">
  <img height=200 img src=./readme_assets/m3655.PNG/>
</p>

**`flag{f17cf5c1e2e94ddb62b98af0fbbd46e1}`**

***M Three Sixty Five - The President***

*One of the users in this environment seems to have unintentionally left some information in their account details. Can you track down The President?*

Using `Get-AADIntUsers` we get the flag for part 4.

<p align="left">
  <img height=200 img src=./readme_assets/m3655.PNG/>
</p>

**`flag{1e674f0dd1434f2bb3fe5d645b0f9cc3}`**


## Tools

- `aadinternals` 
- `powershell`
