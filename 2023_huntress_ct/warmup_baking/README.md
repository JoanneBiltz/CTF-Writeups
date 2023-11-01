# Baking (warmup, 1088 solves, 50 points)

## Introduction

<p align="left">
  <img height=400 img src=./readme_assets/baking-challenge.PNG/>
</p>

## Solution

On the website you have an oven with different items to choose from, one being `Magic Cookies`. Choose Magic Cookies and use Inspect to bring up the dev tools.

You need to change the `cookie` date to get the cookies to finish baking. The cookie value is in `base64`.

`eyJyZWNpcGUiOiAiTWFnaWMgQ29va2llcyIsICJ0aW1lIjogIjEwLzEyLzIwMjMsIDEzOjU5OjEwIn0=`
Converts to `{"recipe": "Magic Cookies", "time": "10/12/2022, 13:29:27"}`

Change the date to `2022` and paste the `base64` code back into the cookie in the dev tools.
`eyJyZWNpcGUiOiAiTWFnaWMgQ29va2llcyIsICJ0aW1lIjogIjEwLzEyLzIwMjIsIDEzOjI5OjI3In0=`

Refresh the page and you will get the flag.

<p align="left">
  <img height=300 img src=./readme_assets/baking-flag.PNG/>
</p>

## Flag

**`flag{c36fb6ebdbc2c44e6198bf4154d94ed4}`**

## Tools

- `base64`


