!!! warning "[This documentation is still under development. Click here to contribute](https://github.com/ZMonk91/DragonRuby-Docs)"
# Publishing Your Game#
---
  Once you've built your game, you're all set to deploy! Good luck in
  your game dev journey and if you get stuck, come to the Discord
  channel!

## 1. Create a new game in Itch.io#
---

  - Log in and create a new game [Here](https://itch.io/game/new).

    |Section|Description|
    |--|--|
    |Title|This value represents your `gametitle`|
    |Project URL| This value represents your `gameid`|
    |Classification| Keep this as `Game`|
    |Kind of Project| Select `HTML` from the drop down list. Dont worry about the HTML project type `_aslo supports binary downloads_`|
    |Uploads| Skip this section for now|
    |Embed Options| Set the dropdown value to `Click to launch in fullscreen`. ** Do NOT use the **  ` Embed in page ` ** option. iFrames are not reliable with regards to capturing input **|

   You can fill out all the other options later.

## 2. Update your metadata#
---

   Point your text editor at mygame/metadata/game_metadata.txt and
   make it look like this: (Remove the `#` at the beginning of each line).

```
devid=bob
devtitle=Bob The Game Developer
gameid=mygame
gametitle=My Game
version=0.1
```
|Item|Description|
|--|--|
|`devid`|The username you use to log into Itch.io|
|`devtitle`|Your name or company name (it can contain spaces)|
|`gameid` |The Project URL value (see details in STEP 1)|
|`gametitle`|The name of your game (it can contain spaces)|
|`version` |Can be any `major.minor` number format|

<br>

## 3. Build your game for distribution.#
---

   Open up the terminal and run this from the command line:<br>
`./dragonruby-publish --only-package mygame`<br>
   (if you're on Windows, don't put the `./` on the front)

   A directory called `./build` will be created that contains your
   binaries. You can upload this to Itch.io manually. <br>For the HTML
   version of your game after you upload it. Check the checkbox labeled
   `This file will be played in the browser`

   For subsequent updates you can use an automated deployment to Itch.io:<br>
     `./dragonruby-publish mygame`

   DragonRuby will package _and publish_ your game to itch.io! Tell your
   friends to go to your game's very own webpage and buy it!

   If you make changes to your game, just re-run dragonruby-publish and it'll
   update the downloads for you.


