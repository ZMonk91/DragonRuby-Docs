# Hello World Tutorial Pt. 2
By [Ryan 'The Juggernaut' Gordon](https://en.wikipedia.org/wiki/Ryan_C._Gordon)

Now let's spice this up a little.

We're going to add some graphics. Each 2D image in DragonRuby is called a
"sprite," and to use them, you just make sure they exist in a reasonable file
format (png, jpg, gif, bmp, etc) and specify them by filename. The first time
you use one, DragonRuby will load it and keep it in video memory for fast
access in the future. If you use a filename that doesn't exist, you get a fun
checkerboard pattern!

There's a "dragonruby.png" file included, just to get you started. Let's have
it draw every frame with our text:

``` ruby

  def tick args
    args.outputs.labels << [ 580, 400, 'Hello World!' ]
    args.outputs.sprites << [ 576, 100, 128, 101, 'dragonruby.png' ]
  end

```

(ProTip: you don't have to restart DragonRuby to test your changes; when you
save main.rb, DragonRuby will notice and reload your program.)

That `.sprites` line says "add a sprite to the list of sprites we're drawing,
and draw it at position (576, 100) at a size of 128x101 pixels". You can
find the image to draw at dragonruby.png.

Quick note about coordinates: (0, 0) is the bottom left corner of the screen,
and positive numbers go up and to the right. This is more "geometrically
correct," even if it's not how you remember doing 2D graphics, but we chose
this for a simpler reason: when you're making Super Mario Brothers and you
want Mario to jump, you should be able to add to Mario's y position as he
goes up and subtract as he falls. It makes things easier to understand.

Also: your game screen is _always_ 1280x720 pixels. If you resize the window,
we will scale and letterbox everything appropriately, so you never have to
worry about different resolutions.

Ok, now we have an image on the screen, let's animate it:

``` ruby

  def tick args
    args.state.rotation ||= 0
    args.outputs.labels << [ 580, 400, 'Hello World!' ]
    args.outputs.sprites << [ 576, 100, 128, 101, 'dragonruby.png', args.state.rotation ]
    args.state.rotation -= 1
  end

```

Now you can see that this function is getting called a lot!

Here's a fun Ruby thing: `args.state.rotation ||= 0` is shorthand for "if
args.state.rotation isn't initialized, set it to zero." It's a nice way to
embed your initialization code right next to where you need the variable.

`args.state` is a place you can hang your own data and have it survive past the
life of the function call. In this case, the current rotation of our sprite,
which is happily spinning at 60 frames per second. If you don't specify
rotation (or alpha, or color modulation, or a source rectangle, etc),
DragonRuby picks a reasonable default, and the array is ordered by the most
likely things you need to tell us: position, size, name.

One thing we decided to do in DragonRuby is not make you worry about delta
time: your function runs at 60 frames per second (about 16 milliseconds) and
that's that. Having to worry about framerate is something massive triple-AAA
games do, but for fun little 2D games? You'd have to work really hard to not
hit 60fps. All your drawing is happening on a GPU designed to run Fortnite
quickly; it can definitely handle this.

Since we didn't make you worry about delta time, you can just move the
rotation by 1 every time and it works without you having to keep track of
time and math. Want it to move faster? Subtract 2.

Now, let's move that image around.

``` ruby

  def tick args
    args.state.rotation ||= 0
    args.state.x ||= 576
    args.state.y ||= 100

    if args.inputs.mouse.click
      args.state.x = args.inputs.mouse.click.point.x - 64
      args.state.y = args.inputs.mouse.click.point.y - 50
    end

    args.outputs.labels << [ 580, 400, 'Hello World!' ]
    args.outputs.sprites << [ args.state.x, args.state.y, 128, 101, 'dragonruby.png', args.state.rotation ]

    args.state.rotation -= 1
  end

```

Everywhere you click your mouse, the image moves there. We set a default
location for it with args.state.x ||= 576, and then we change those variables
when we see the mouse button in action. You can get at the keyboard and game
controllers in similar ways.

There is a lot more you can do with DragonRuby, but now you've already got
just about everything you need to make a simple game. After all, even the
most fancy games are just creating objects and moving them around. Experiment
a little. Add a few more things and have them interact in small ways. Want
something to go away? Just don't add it to args.output anymore.