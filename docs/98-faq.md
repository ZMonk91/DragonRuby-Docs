# Frequently Asked Questions#
---
??? question "Where do I start?"
    1. Start with the readme.txt file and follow the instructions in there based on your experience level.
    2. The next thing you want to look at is the [CheatSheet](/97-cheatsheet) and skim it.
    3. Go to mygame/documentation for a collection of markdown files that expand on what's in cheetsheet.txt.
    4. Go through the samples under the samples directory in order. They increase in difficulty. Within each sample is an api listing of what was used.
    5. There is a file called `ctags-emacs` that contains all internal functions in DragonRuby. If you can't find what you need in the locations above, go there for a hint about something that might help you and ask @amirrajan to elaborate.
    6. You'll also what to check out [the Github](the api you have a question about might be open source).
    7. There are documentation contributions by the community [here](http://tinyurl.com/dragonruby-gtk-docs).

??? question "Is DragonRuby-GTK OpenSource?"

    Parts of the engine are open source (MIT) and can be found on [Github](https://github.com/DragonRuby/dragonruby-game-toolkit-contrib). We cannot legally open source all of DragonRuby because of NDA agreements with game console manufacturers. If there is something you'd like to see the source for, just ask **@amirrajan** and he'll see if he can accommodate it.

??? question "Does DragonRuby support Gems? What version of Ruby is DragonRuby?"

    #### **Definition of Terms**
    A bit of context/clarification is needed before answering this question. The general definition of **Ruby** (or any language for that matter) isn't sufficient when answering this question in detail. We have to split **Ruby** into three separate things. The **Language Specification**, the **Runtime**, and the **Core Libraries**.
    #### **Language Specification**
     This represents the language's semantics and syntax (how the language is parsed). For example, Ruby 1.9 does not support keyword arguments, Ruby 2.0 does. Ruby 3.0 deprecates the "last argument as a Hash" parsing and forces you to use the double splat operator.
    #### **Runtime** 
    This represents the unique implementation/execution. Examples of Runtimes that implement Ruby's Language Specification are: MRI, mRuby, JRuby, Truffle, Artichoke, Opal.
    #### **Core Libraries**
    This represents the libraries/classes that are supported for a specific runtime. For example: MRI Ruby's core libs are different that JRuby's core libs, which are both different from mRuby's corelibs, etc.
    #### **Applying These Terms to DragonRuby**
    With the clarification of terms above. 

    1. DragonRuby is compatible with Ruby 2.0's Language Specification.
    2. DragonRuby's Runtime is inspired by what's been learned over the past 25 years of MRI. It's inspired by mRuby, Objective C, C++, LLVM, NodeJS, Erlang, and Clojure. The specific inspirations are varied, nuanced, and evolving (feel free to asking questions in #general if you want specific).
    3. DragonRuby's Core Libraries are constrained by what can be implemented in a portable fashion and takes a strong dependency on libSDL2 and other portable C libraries.
    Now to Answer the Question About Gems
    DragonRuby's Ruby will eventually have gem capabilities, but it's unlikely that you'll be able to use MRI based gems, JRuby gems, et al. So when DragonRuby has a gem cli app, the only gems that will work will be those that were explicitly designed for DragonRuby. We also cannot use MRI's gem binary because it isn't portable (MRI assumes a conventional file system which is not the case for the platforms we target.
    What will DragonRuby's Gems Look Like
    DragonRuby's gem architecture will mostly likely depend on things like CocoaPods for iOS/Mac, Gradle for Android, mRuby's gem architecture, and CLibs. This is a lot of work...
    Stopgap Until we Have Gems
    If there's an MRI gem that you'd like to leverage. Let @amirrajan know and he'll add it to #feature-requests.

??? question "Does DragonRuby have a REPL/IRB?"
    You can use DragonRuby's Console within the game to inspect object and execute small pieces of code. For more complex pieces of code create a file called repl.rb and put it in mygame/app/repl.rb: 
    1. Any code you write in there will be executed when you change the file. You can organize different pieces of code using the repl method:
      ``` ruby
      repl do
        puts "hello world"`
        puts 1 + 1
      end
      ```

    2. If you use the repl method, the code will be executed and the DragonRuby Console will automatically open so you can see the results (on Mac and Linux, the results will also be printed to the terminal).
    3. All puts statements will also be saved to logs/log.txt. So if you want to stay in your editor and not look at the terminal, or the DragonRuby Console, you can tail this file.
    4. To ignore code in repl.rb, instead of commenting it out, prefix repl with the letter x and it'll be ignored.
    ``` ruby
    # This code will be executed when you save the file.#
    ---
    repl do
      puts "Hello"
    end

    repl do
      puts "This code will also be executed."
    end

    # use xrepl to "comment out" code#
    ---
    xrepl do
      puts "This code will not be executed because of the x infront of repl".
    end
    ```

??? question "Does DragonRuby support C Extensions?"
    Eventually yes. But it will be a "Pro" feature and require some form of subscription. Maintaining the compilation toolchain has an ongoing upkeep and a recurring subscription is the only way this work can be sustainably done. The pricing model will be fair I promise. If you're interested in creating C Extensions, DM @amirrajan and we'll figure out something that works for both of us (especially if you can't afford to pay the subscription if/when this happens).

??? question "Does DragonRuby support Pry?"

    **IMPORTANT** You must first read the "Does Dragonruby support Gems" section to get a bit of context. The following answer assumes you've read this.<br>
    Pry is a gem that assumes you are using the MRI Runtime (which is incompatible with DragonRuby). Eventually DragonRuby will have a pry based experience that is compatible with a debugging infrastructure called LLDB. Take the time to read about LLDB as it shows the challenges in creating something that is compatible. <br>
    **Stopgap**
      1. DragonRuby is hot loaded which gives you a very fast feedback loop (if the game throws an exception, it's because of the code you just added). 

      2. Use ./dragonruby mygame --record to create a game play recording that you can use to find the exception (you can replay a recoding by executing ./dragonruby mygame --replay last_replay.txt or through the DragonRuby Console using $gtk.recording.start_replay "last_replay.txt".

      3. DragonRuby also ships with a unit testing facility. Take a look at samples/99_zz_gtk_unit_tests to see how you can create your own unit tests.

    4. Get into the habit of adding debugging facilities within the game itself. You can add drawing primitives to args.outputs.debug that will render on top of your game but will be ignored in a production release.

    5. Debugging something that runs at 60fps is (imo) not that helpful. The exception you are seeing could have been because of a change that occurred many frames ago. 
    <br>

    We know these stopgaps aren't ideal. But a debugger is essentially a mechanism that manipulates a Runtime's virtual machine at its core. So it'll take time to get right, and ensure that it's useful for real time apps.
??? question "What is `args.state.new_entity (OpenEntity)` or`args.state.new_entity_strict (StrictEntity)`? When should I use it over Arrays, Hashes, and Classes?"

    The Entity type's underlying interface is a Hash. Using entity.hash gives you by reference access to the Entity. This is why the method isn't called to_h which communicates that a new object would be created.  <br>
    **TODO**: Write more stuff about entities

??? question "What are the `Kernel.caller_locations`?"

    We are dealing with a hot loaded environment where the code could be written in a file, saved, then removed. We are also dealing with OS'es that don't even have a concept of a conventional file system. This is further "complected" because of native interop, AOT compilation, and bytecode compilation. Don't expect this to happen.

??? question "Performance Issues"
    1. If you're using Arrays for your primitives (`args.outputs.sprites << []`), use Hash instead (`args.outputs.sprites << { x: ... }`).
    2. If you're using Entity for your primitives (`args.outputs.sprites << args.state.new_entity`), use `StrictEntity` instead (`args.outputs.sprites << args.state.new_entity_strict`).
    3. Use `.each` instead of `.map` if you don't care about the return value.
    4. When concatenating primitives to outputs, do them in bulk. Instead of:

    ``` ruby
    args.state.bullets.each do |bullet|
      args.outputs.sprites << bullet.sprite
    end
    ```
    
    do

    ``` ruby
    args.outputs.sprites << args.state.bullets.map do |b|
      b.sprite
    end
    ```

    5. Use args.outputs.static_ variant for things that don't change often (take a look at the Basic Gorillas sample app and Dueling Starships sample app to see how static_ is leveraged.
    6. Consider using a render_target if you're doing some form of a camera that moves a lot of primitives (take a look at the Render Target sample apps for more info).
