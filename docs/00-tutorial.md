# Getting Started
 The following are sections designed to cater to your experience level. 
 If you are not sure where to start, try out the Beginner section and adjust depending on how easy it is for you.<br><br>
  [Beginner](#beginner) - No Programming Experience <br> 
  [Intermediate](#intermediate) - Familiar with Unity/GML<br>
  [Advanced](#advanced) - Familiar with Dynamically Typed Languages<br>

### Beginner#
*Recommended for individuals with no programming experience*<br>
   If you have no programing experience at all. You'll want to take the
   time to see what DragonRuby is like before jumping in to code. Watch
   the following videos in order (each one is only ~20 minutes long).

   ** Don't attempt to code anything shown in the video yet, just watch them to
   get familiar with the language and how games are built. **

  1. [Beginner Introduction to Ruby](https://www.youtube.com/watch?v=ixw7TJhU08E)
  1. [Intermediate Introduction to Ruby Syntax](https://www.youtube.com/watch?v=HG-XRZ5Ppgc)
  1. [Intermediate Introduction to Arrays in Ruby](https://www.youtube.com/watch?v=N72sEYFRqfo)

   Once you have watched all the videos. Then (and only then) go back
   through the videos and follow along. 

  |Sample|Location|
  |--|--|
  |Beginner Introducation to Ruby|`samples/00_beginner_ruby_primer`|
  |Intermediate Introduction to Ruby Syntax|`samples/00_intermediate_ruby_primer`|
  |Intermediate Introduction to Arrays in Ruby|`samples/00_intermediate_ruby_primer`|
  
  <br>

### Intermediate#
*Recommended for individuals familiar with C#(Unity) or GML(GameMaker) but new to Ruby*<br>

   Those engines rot your brain. Forget the concepts that the forced you
   to learn. Game development is so much simpler than what they make you
   do. Please, try your best to set aside the concepts those engines
   teach (we promise our approach to game development is much much easier).

   Watch these videos to get familiar with the Ruby language and
   programming environment (they are ~20 min each so it'll be quick):

   1. [Beginner Introduction to Ruby](https://www.youtube.com/watch?v=ixw7TJhU08E)
   2. [Intermediate Introduction to Ruby Syntax](https://www.youtube.com/watch?v=HG-XRZ5Ppgc)
   3. [Intermediate Introduction to Arrays in Ruby](https://www.youtube.com/watch?v=N72sEYFRqfo)

   You may also want to try this free course provided at [DragonRuby School](http://dragonruby.school)

   After you've watch the videos, you'll be ready for the Advanced Tutorial


### Advanced#
*Recommended for individuals familia with Dynamically Typed Languages (Ruby, Lua, Python, or JavaScript)*<br>

1. Work through [this Hello World Tutorial](96-hello-world.md)
1. Skim through the [CheatSheet](97-cheatsheet.md) to get a feel for some of the other API's you have access to. If you never even more detail, you'll find them on the left hand side of these pages.
1. Run each sample app in order and read the code. * The sample apps are located in the `sample` directory and are ordered by increasing complexity. Run each one of them and read through the
    code. Play around by changing values and see how they change the game. *
1. Integrate your editor. There is a file called `vim-ctags` and `emacs-ctags`. The data in
    these files are standard output provided by Exuberent CTAGS. Most
    editors have a "ctags plugin" so just search for that plugin for your
    editor and point it to these files.
1. Get in the habit of reading the CHANGELOG. We are constantly adding new features to the engine. Be sure to read the changelog with every release.

## Publishing Your Game
  Once you've built your game, you're all set to deploy! Good luck in
  your game dev journey and if you get stuck, come to the Discord
  channel!

** STEP 1: Create a new Game in Itch.io.

   Log into Itch.io and go to https://itch.io/game/new.

   - Title: Give your game a Title. This value represents your `gametitle`.
   - Project URL: Set your project url. This value represents your `gameid`.
   - Classification: Keep this as Game.
   - Kind of Project: Select HTML from the drop down list. Dont worry,
     the HTML project type _aslo supports binary downloads_.
   - Uploads: Skip this section for now.
   - Embed Options: Set the dropdown value to "Click to launch in fullscreen".
     DO NOT use the Embed in page option. iFrames are not reliable with
     regards to capturing input.

   You can fill out all the other options later.

** STEP 2: Go to mygame/metadata/metadata.txt and update it.

   Point your text editor at mygame/metadata/game_metadata.txt and
   make it look like this: (Remove the `#` at the beginning of each line).

   #+begin_src text
   devid=bob
   devtitle=Bob The Game Developer
   gameid=mygame
   gametitle=My Game
   version=0.1
   #+end_src

   The `devid` property is the username you use to log into Itch.io.
   The `devtitle` is your name or company name (it can contain spaces).
   The `gameid` is the Project URL value (see details in STEP 1).
   The `gametitle` is the name of your game (it can contain spaces).
   The `version` can be any `major.minor` number format.

** STEP 3: Build your game for distribution.

   Open up the terminal and run this from the command line:

   #+begin_src sh
     ./dragonruby-publish --only-package mygame
   #+end_src

   (if you're on Windows, don't put the "./" on the front. That's a Mac and
   Linux thing.)

   A directory called `./build` will be created that contains your
   binaries. You can upload this to Itch.io manually. For the HTML
   version of your game after you upload it. Check the checkbox labeled
   "This file will be played in the browser".

   For subsequent updates you can use an automated deployment to Itch.io:

   #+begin_src sh
     ./dragonruby-publish mygame
   #+end_src

   DragonRuby will package _and publish_ your game to itch.io! Tell your
   friends to go to your game's very own webpage and buy it!

   If you make changes to your game, just re-run dragonruby-publish and it'll
   update the downloads for you.


