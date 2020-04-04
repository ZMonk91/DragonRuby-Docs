# Making A Button
[!embed?max_width=1050&max_height=1050](https://www.youtube.com/watch?v=Gm1qJZPkj5M)

??? note "View Finished Source Code"

    ``` ruby
    class Button
      attr_accessor :outputs, :inputs

      def DisplayButton(x, y, text)
        button_border = [x, y, 150, 150, 0, 0, 128]
        button_label = [x + 50, y + 75, text]
        outputs.borders << button_border
        outputs.labels << button_label

        if inputs.mouse.click
          if inputs.mouse.click.point.inside_rect? button_border
            outputs.labels << [200, 300, "Clicked"]
          end
        end
      end
    end

    def tick args
      $button = Button.new
      $button.outputs = args.outputs
      $button.inputs = args.inputs
      $button.DisplayButton(500, 400, "Click")
    end
    ```

## Creating a class 
   Begin by deleting everything inside `mygame/app/main.rb` so we can start from a blank slate. Let's begin by creating a class called `Button`

  ``` ruby 
  class Button
  end
  ```
  This is similar to any other Object Oriented Language, where we are defining our class.
  Directly underneat it, with a tab space, add the attribute that allows us to get and set instance variables, with `attr_accessor`. Let's include the DragonRuby's `outputs` and `inputs` methods. 
  ``` ruby 
  class Button
  ```
  {== `attr_accesor :outputs, :inputs` ==}
  ``` ruby
  end
  ```
  We can now access the `outputs` and `inputs` methods defined within the engine. These handle the I/O and Rendering.
## Defining a method
  Let's begin creating the method for displaying our button. On a new line (inside the Button class), define the `DisplayButton` method.
  ``` ruby 
  class Button
  attr_accesor :outputs, :inputs
  ```
    {==`def DisplayButton`<br>
    `end` ==}
  ``` ruby
  end
  ```

## Adding Parameters
Let's add parameters to it. There are two ways to handle this. The first way is to write `(x,y, text)` and the second is to just write `x y text`. **Both ways are valid in Ruby**. For this tutorial, we will use the parenthesis approach. <br>
As you can see, we are not defining the types for these variables. That is because Ruby is a dynamically typed language, just like Python. The x variable will be our x position and the y will be our y position. The text variable will be our string value.<br>
*The `x` and `y` values will automatically be inferred as an integer unless we use floating point values.*
  ``` ruby 
  class Button
  attr_accesor :outputs, :inputs
  ```
  &nbsp;&nbsp;&nbsp;&nbsp;  `#!ruby def DisplayButton`{==`#!ruby (x, y, text)`==}<br>
  ``` ruby
    end

  end
  ```

## Adding variables, borders, and labels
Now let's assign some array values into our own variables for the border and labels. The values we are going to assign to our border will look like this:<br> `#!ruby [x position, y position, width, height, red, green, blue]` <br> Let's add our own border:<br> `#!ruby button_border = [x, y, 150, 150, 0, 0, 128]`

For the border, the values we are going to assign will look like this:<br> `#!ruby [x position, y position, text value]`<br> Let's add our own label:<br>
`#!ruby button_label = [x + 50, y + 75, text]`

Your code should now look like this:
  ``` ruby 
  class Button
  attr_accesor :outputs, :inputs

    def DisplayButton(x, y, text)
  ```
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; {==`#!ruby button_border = [x, y, 150, 150, 0, 0, 128]`==}<br>
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  {==`#!ruby button_label = [x + 50, y + 75, text]`==}
  ``` ruby
    end

  end
  ```
  Now we need to assign our new array variables to the engine's output methods in order to have the engine display our new border and label.<br> To do this, we need to call DragonRuby's `outputs.borders` and `outputs.labels` respectively. Then assign the array's using `<< ARRAY`. <br> Our code should look like this: <br>

  ``` ruby 
  class Button
  attr_accesor :outputs, :inputs

    def DisplayButton(x, y, text)
      button_border = [x, y, 150, 150, 0, 0, 128]
      button_label = [x + 50, y + 75, text]
  ```
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; {==`#!ruby outputs.borders << button_border`==}<br>
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  {==`#!ruby outputs.labels << button_label`==}
  ``` ruby
    end
  end
  ```

## Adding Click Events
Now for the tricky part. We need to register our click events. This will require a nested if statement because we need to check for a regular click event, then check if it happens within the border of our button. <br>
To do this, we need to listen for the click event from the mouse:<br>
`#!ruby if inputs.mouse.click`
<br>Then from within that if statement, we need to check if we are clicking inside of the rectangle from an object that is of the type `rect`, like this: 

`#!ruby if inputs.mouse.click.point.inside_rect?(button_border)`<br>
*The `?` denotes that that this is nullable.*

The last thing we need to do is to write the action we want to happen once our button is clicked. Within your second `if` statement, write:<br> `!#ruby outputs.labels << [200, 300, "Clicked"]`<br>
This will generate a new label to tell us if our button was clicked.  Your code should now look like this:<br>
```
class Button
  attr_accessor :outputs, :inputs

  def DisplayButton(x, y, text)
    button_border = [x, y, 150, 150, 0, 0, 128]
    button_label = [x + 50, y + 75, text]
    outputs.borders << button_border
    outputs.labels << button_label
```

  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; {==`#!ruby if inputs.mouse.click`==}<br>
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; {==`#!ruby if inputs.mouse.click.point.inside_rect?(button_border)`==}<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{==`outputs.labels << [200, 300, "Clicked"]`==}
``` ruby
      end
    end
  end
end

```

## Begin looping
We're not done yet! We have finished the implementation details, now we just need to define the tick method for our main method. This will call the code and begin running it as we intended to. <br>
On a new line, outside of `class Button` block, define your tick method like this: <br>
`#!ruby def tick args`
This is our main update loop. The `args` is just an informal name for arguments, which we will soon make heavy use of. 
Code check:<br>
``` ruby
class Button
  attr_accessor :outputs, :inputs

  def DisplayButton(x, y, text)
    button_border = [x, y, 150, 150, 0, 0, 128]
    button_label = [x + 50, y + 75, text]
    outputs.borders << button_border
    outputs.labels << button_label

    if inputs.mouse.click
      if inputs.mouse.click.point.inside_rect? button_border
        outputs.labels << [200, 300, "Clicked"]
      end
    end
  end
end
```

{==`#!ruby def tick args` ==}<br>
{== `#!ruby end` ==}

## Creating Instances
On a new line, inside of your `#!ruby def tick args` function, create a new instance of your button using `#!ruby $button = Button.new` <br> This creates an instance of our new `Button` class. The `$` indicates that this is a global variable.

Now on a new line, write <br> `#!ruby $button.outputs = args.outputs` <br>to specify that the `attr_accessor` called  `outputs` is the same as the arg's `outputs`. 

Let's include the `inputs` as well, using <br> `#!ruby $button.inputs = args.inputs`
 
 Your code should now look like this:

``` ruby
 class Button
  attr_accessor :outputs, :inputs

  def DisplayButton(x, y, text)
    button_border = [x, y, 150, 150, 0, 0, 128]
    button_label = [x + 50, y + 75, text]
    outputs.borders << button_border
    outputs.labels << button_label

    if inputs.mouse.click
      if inputs.mouse.click.point.inside_rect? button_border
        outputs.labels << [200, 300, "Clicked"]
      end
    end
  end
end

def tick args
```
&nbsp;&nbsp;{==`#!ruby $button = Button.new`==}<br>
&nbsp;&nbsp;{==`#!ruby $button.outputs = args.outputs`==}<br>
&nbsp;&nbsp;{==`#!ruby $button.inputs = args.inputs`==}<br>
`end`

Lastly, we need to call the `DisplayButton` we defined in the `Button` class using <br> `#!ruby $button.DisplayButton(500, 400, "Click")` <br>

# Running your program
There we have it. You can now click on the `DragonRuby.exe` to run your new program. Try clicking inside yuor new button to quickly flash the text telling us that the coked worked correctly.

As a final challenge, go through the DragonRuby's documentation and try to figure out how to add images to your `DisplayButton` method. Make is so after clicking, the text will stay shown while the button is being pressed. Try fixing the alignment bug that is present on the text if you use longer text phrases.

Your final code (without the challenges) should now look like this:

```ruby
class Button
  attr_accessor :outputs, :inputs

  def DisplayButton(x, y, text)
    button_border = [x, y, 150, 150, 0, 0, 128]
    button_label = [x + 50, y + 75, text]
    outputs.borders << button_border
    outputs.labels << button_label

    if inputs.mouse.click
      if inputs.mouse.click.point.inside_rect? button_border
        outputs.labels << [200, 300, "Clicked"]
      end
    end
  end
end

def tick args
  $button = Button.new
  $button.outputs = args.outputs
  $button.inputs = args.inputs
  $button.DisplayButton(500, 400, "Click")
end

```