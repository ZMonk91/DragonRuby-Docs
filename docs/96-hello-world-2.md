# Hello World Tutorial Pt. 2
By [Ryan 'The Juggernaut' Gordon](https://en.wikipedia.org/wiki/Ryan_C._Gordon)

Do you know what an if statement is? A for-loop? An array? That's all you'll
need to start.

Ok, here are few rules with regards to game development with GTK:

- Your game is all going to happen under one function...
- ...that runs 60 times a second...
- ...and has to tell the computer what to draw each time.

That's an entire video game in one run-on sentence.

Here's that function. You're going to want to put this in mygame/app/main.rb,
because that's where we'll look for it by default. Load it up in your favorite
text editor.

``` ruby
  def tick args
    args.outputs.labels << [ 580, 400, 'Hello World!' ]
  end
```

Now run `dragonruby` ...did you get a window with "Hello World!" written in
it? Good, you're officially a game developer!

`mygame/app/main.rb`, is where the Ruby source code is located. This looks a little strange, so
I'll break it down line by line. In Ruby, a '#' character starts a single-line
comment, so I'll talk about this inline.

``` ruby

  # This "def"ines a function, named "tick," which takes a single argument
  #  named "args". DragonRuby looks for this function and calls it every
  #  frame, 60 times a second. "args" is a magic structure with lots of
  #  information in it. You can set variables in there for your own game state,
  #  and every frame it will updated if keys are pressed, joysticks moved,
  #  mice clicked, etc.
  def tick args

    # One of the things in "args" is the "outputs" object that your game uses
    #  to draw things. Afraid of rendering APIs? No problem. In DragonRuby,
    #  you use arrays to draw things and we figure out the details.
    #  If you want to draw text on the screen, you give it an array (the thing
    #  in the [ brackets ]), with an X and Y coordinate and the text to draw.
    #  The "<<" thing says "append this array onto the list of them at
    #  args.outputs.labels)
    args.outputs.labels << [ 580, 400, 'Hello World!' ]
  end

```

Once your `tick` function finishes, we look at all the arrays you made and
figure out how to draw it. You don't need to know about graphics APIs.
You're just setting up some arrays! DragonRuby clears out these arrays
every frame, so you just need to add what you need _right now_ each time.

