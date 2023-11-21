# Syncopated Beat (stego)

## Introduction

<p align="left">
  <img height=700 img src=./readme_assets/beat-challenge.PNG/>
</p>

> We know there's a hidden message somewhere here, but none of our steg tools are able to reveal it. Maybe we need to think outside the box? It is a well-known fact that rock musicians are all Non-Incarnate Conscious Entities (NICEs) influenced. NICEs speak lyrics to them and insinuate their evil messages into the song.

You are given two .wav files, Syncopated-Beat.wav and mysterious_music.wav.

## Solution

mysterious_music.wav has some distortion in the beginning of the song. I tried running it through QSSTV but didn't get anything usable.

Listening to the audio file Syncopated-Beat.wav, halfway through a voice is heard but it sounds backwards.

Open the file in `Audacity` and find the area where it is playing backwards and select it. Use `effects/reverse` to reverse the audio. 
Listen to the reversed audio and get a hint. 

 It says to use the stego program used by Elliot in Mr Robot on the 2nd audio file. The flag is the name of the new CTO, all caps and no spaces.
 
<p align="left">
  <img height=700 img src=./readme_assets/sync-reversed.PNG/>
</p>

Mr Robot use [DeepSound](https://jpinsoft.net/deepsound/overview.aspx).

Googling the new CTO from Mr Robot we find Tyrell Wellick. Use this for the password in deepsound.

Extract the hidden jpg for the flag.

<p align="left">
  <img height=700 img src=./readme_assets/ozzy-mandias.jpeg/>
</p>


## Flag

**`flag{Lookout_COVID_BATZ!!!}`**

## Tools

- [Audacity](https://www.audacityteam.org/download/)
- [DeepSound](https://jpinsoft.net/deepsound/overview.aspx)



