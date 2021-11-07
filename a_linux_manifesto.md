## Overview

I'm sure it's no secret to you at this point that I run Linux on basically every machine I do work on.

Most of it comes down to

- me being a nerd
- being stubborn and not giving up the platform I started writing code on

However, there's a lot of good reasons to run Linux on a development machine. Now, I'm not going to
sit here and try to tell you that you should be installing Linux on absolutely every machine you use for gaming _(I'll
let the Linux forums do that for me :) )_, but I will go over what are, in my opinion, are the reasons to run Linux for
writing code.

### Freedom

Windows, being an operating system whose target market is basically "everyone alive", has a lot of safeguards built into
it to make sure that you don't accidentally brick your OS, should you be mucking about in system-critical areas.

This is both a benefit and a drawback, in my opinion. If you're just trying to do some simple task that you aren't aware
could have serious repercussions for your system, it can be nice to have the system prevent you from doing something
potentially dangerous. However, if you're trying to do something major to your system that you know you need to do, and
you know what you're doing, Window's prevention systems can feel a bit infantilizing.

Linux, for better or for worse, will allow you to do basically anything you want to it, up to and including bricking
your system entirely.

We'll get into the power of the command line later, but it should be taken into consideration (especially in contrast to
Windows' safeguards) that the command for wiping absolutely everything off of your system, yes I'm absolutely sure, is
only a handful of characters:

```bash
  # Remove, recursively and forcibly, everything from the root directory
  $ rm -rf /*
```

This sounds like a recipe for disaster, but so long as you don't get careless when you're typing in commands, and think
about what you've written before you hit Enter, you should be just fine.

This freedom, in contrast to a more locked-down OS, offers you far more flexibility in terms of customizing your system
to be completely yours, allowing you to install any software you want, modify any software currently running on your
machine, change the structure of the filesystem -- anything you can dream of, Linux will almost certainly let you do it.

Whether or not doing it is a good idea, well, that's up to you.

### The Command Line

GUIs are like, so last year.

The command line, as the name might suggest, is a means of issuing commands to your computer. There are commands for
moving files around (`mv`), copying files from one place to another, (`cp`), compiling code (`gcc, make, etc.`), and
many more.

This might sound like a more cumbersome way to do things on your system, but it can be ruthlessly efficient in many
cases.

Say you've set up a nice project folder for a Python project you've been working on for a little while. All of your source
code files are contained in the main project folder, as well as all of the documentation you've written for them -- you
are writing documentation for your code, right?

Say the project has matured quite a bit, and having all of your files in one folder is getting a bit cumbersome. You
decide to organize your files into two separate sub-folders: `src` for source code files _(e.g. main.py)_, and `doc` for
documentation files _(e.g. ClassName.txt)_

What's the easiest and fastest way to organize all of these files into each folder?

If you're using a GUI, you've really got no other option except to select all of the source code files by hand, drag
them over to `src`, and then do the same with the documentation files.

This is slow and painful. This kills the man.

Let's see what we can do with the command line.

First, let's open a command line session in our project folder.

```bash
  # Change the current directory to "my_python_project"
  $ cd my_python_project 
```

As a convention, the command you want to run always comes first in the command -- then, you specify all of the input you
want to give to that command (typically called the "arguments")

Next, let's create a new folder `src`, and move all of our source code files there.

```bash
  # Make a new directory called "src"
  $ mkdir src

  # Move all files in the current directory ending in ".py" to the directory "src"
  $ mv *.py src
```

Now, let's do the same for our documentation files.

```bash
  # Make a new directory called "doc"
  $ mkdir doc

  # Move all files in the current directory ending in ".txt" or ".doc" to the directory "src"
  $ mv *.txt *.doc doc
```

These commands will each complete in a fraction of a second, saving you precious time that you could be using to
actually work on this project.

Let's try another example. Say you've got a really big text file that contains the names of everyone in your town, and
you want to find all of the people named Jerry.

Really important stuff, I know.

We can use the `grep` command to search this file for all lines that contain the string "Jerry":

```bash
  # Print all lines containing the word "Jerry" from the file "list_of_names.txt"
  $ grep "Jerry" list_of_names.txt 
```

Command line interfaces, while not visually striking, allow you to be incredibly precise about what you want to do, and
offer a lot of power to control your system.

You're not limited to running just one command at a time, however. The command line gets even better when you learn how
to chain commands together.

Let's say that you've got a program that you've written that has a lot of log output that's a pain to sort through, and
you really only care about log output that contains a certain piece of text, say all lines that say "WARNING".

Well, we know what command we need to run the script (`python myscript.py`), and we know how to search text for specific
strings (`grep`). How do we get these two things to interact?

Introducing: the pipe!

Typically, when you run your program on the command line, all of the output gets written to the screen. However, we can
use something called a pipe to take all of that output that would normally just end up on the screen, and feed it (or
_pipe_ it) into another command.

We can do this like so:

```bash
  Run the python script "myscript.py", and pipe output into the "grep" command, which is looking for the string "WARNING"
  $ python myscript.py | grep "WARNING"
```

That little line in between the two commands tells the shell we're using to take all of the output from our Python
script and pipe it into `grep`, which will then search whatever input it's receiving for lines containing the string
"WARNING", and then print them out to the screen.

This is possible because grep, when not given a file to search, will instead search what's called "standard input" --
this is generally input from the user that's typed in from the user, but when using a pipe, we can redirect the output
of another command to the standard input of `grep`, and have it search over that instead of over a file.

We're not limited to piping just once. Too many WARNING lines being printed out, and you want to search for only WARNING
lines that contain the word "missing"? Slap another pipe onto it!

```bash
  $ python myscript.py | grep "WARNING" | grep "missing"
```

You can chain as many pipes together as you want, with whatever commands you want, so long as the commands being piped
into can accept input from "standard input" _(abbrev. "stdin")_.

### Ease of Setting Up a Development Environment

What all do you need to do to get set up to write Python code in Windows?

Typically, you would open your browser, google some Python runtime for Windows like Anaconda, download it, run the
installer, and then you would use either the built-in Python shell that came with Anaconda if you want a Python REPL, or
you would invoke Anaconda through Command Prompt.

Personally, I find this to ba a bit cumbersome -- there really isn't a central place to download software packages on
Windows for stuff like Python or some major compilers _(at least, that was the case before chocolatey)_, so you're stuck
with opening a browser, and using your own judgement _(or more likely, just using Google's top result)_ to determine
what to use in order to run Python on Windows.

On Linux, getting set up on Python is easy. First, open the command line and install python:

```bash
  # As the super-user, run the "apt" package manager and install the package "python"
  $ sudo apt install python
```

and then...you're done. Now, you can run a Python REPL by just invoking `python` on the command line, and can run Python
scripts by invoking `python` with the name of your script.

Once you're comfortable with the command line, this process is incredibly streamlined -- if you need something, just ask
your operating system's built in software package manager to fetch it for you and install. No need to open a browser,
unless you want to research competing packages that offer similar functionality, or want to learn more about what each
package does.

Sure, a Python IDE _(Integrated Development Environment)_ like PyCharm would solve a lot of this hassle, since it
installs a lot of important dependencies for you, but you shouldn't need to be shackled to an IDE just to be able to 
write code for a specific language; if you want to be able to write Python code in a barebones editor and run it on the
command line, you should be able to do so without a whole lot of fuss.
