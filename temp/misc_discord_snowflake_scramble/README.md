# Discord Snowflake Scramble (misc, 322 solves, 50 points)

## Introduction

<p align="left">
  <img height=400 img src=./readme_assets/discord-challenge.PNG/>
</p>

## Solution

You are given a link to a discord server `https://discord.com/channels/1156647699362361364/1156648139516817519/1156648284237074552`.

When clicking the link you are taken to a server with all channels blurred out and a message.

<p align="left">
  <img height=300 img src=./readme_assets/discord-message.PNG/>
</p>

I tried creating a join link using [dicsordAPI](https://discordapi.com/permissions.html) but was not successful.

`https://discord.com/oauth2/authorize?client_id=1156647699362361364/1156648139516817519/1156648284237074552&scope=bot&permissions=66560`

<p align="left">
  <img height=300 img src=./readme_assets/discord-message2.PNG/>
</p>

Use the discord widget to embed discord into your website, replace your client ID with the challenge discord ID 

`https://www.remote.tools/remote-work/discord-widget`

```
<iframe src="https://discord.com/widget?id=1156647699362361364&amp;theme=dark" width="350" height="500" frameborder="0" sandbox="allow-popups allow-popups-to-escape-sandbox allow-same-origin allow-scripts"></iframe>
```

Paste the code into [html-online](https://html-online.com/editor/) to get a preview. Click the `Join Server` button to join the discord server and get the flag.

<p align="left">
  <img height=300 img src=./readme_assets/discord-flag.PNG/>
</p>

## Flag

**`flag{bb1dcf163212c54317daa7d1d5d0ce35}`**

## Tools

- [dicsordAPI](https://discordapi.com/permissions.html)
- [html-online](https://html-online.com/editor/)
