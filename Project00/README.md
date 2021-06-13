# Setting up your programming environment

The purpose of this project is to get you ready to write code. This
includes having a reasonable version of Python installed and knowing
how to edit and run your Python files.

## Installing Python

If you are running Linux or macOS, you probably already have Python
installed. For the sake of wide applicability, I will try to use
features available as early as Python 3.4, but if you have a more
recent version and know how to use it, you can of course feel free to
do so. If you are on Windows, I suggest you install Ubuntu within the
[Windows Subsystem for
Linux](https://docs.microsoft.com/en-us/windows/wsl/install-win10), at
which point you can follow the Linux installation instructions. The
most general instructions are to go to [the Python
website](https://www.python.org/downloads/) and follow their
instructions. If you are on Mac, you might want to look into
[Homebrew](https://brew.sh/), which is a handy package
manager. Otherwise if you are on Linux, just install Python from your
distribution's package manager. In any case, the installation should
eventually look something like

```
sudo apt install python
```

where I have chosen the `apt` package manager from Debian-based
distros somewhat arbitrarily. On Mac that would look like `brew
install python`, and on FreeBSD `pkg install python`, but the idea is
the same. Regardless, once you think you have Python installed, open a
terminal and type `python --version`. Anything starting with a 3
should be okay, but if you see Python 2.7, try running `python3
--version`. If you have to use `python3`, just remember that for
later.

## Choosing an Editor

Now that you have Python installed, you need a way to edit Python
files, which typically end with the extension `.py`. You can use any
editor that can edit plain text files, but a few suggestions are
[Vim](https://www.vim.org/),
[Emacs](https://www.gnu.org/software/emacs/), and
[VSCode](https://code.visualstudio.com/). Of these, VSCode will be the
easiest to get started with, probably followed by Emacs and Vim. Emacs
has a better graphical interface than Vim, but it is also more
complicated and consequently could be harder to use. Vim is probably
the most confusing initially, but as the simplest editor you may be
able to use it quickly. It will also be installed by default on Mac,
Linux and WSL. I use Emacs with Vim editing keybindings and would
recommend that to everyone, but it would take an entire project on its
own to get that set up. If you're interested, see my [blog
post](https://bwestbro.com/blogs/emacs.html) on setting up Emacs for
Go development, but the Python version would be substantially
different. You can also use more basic editors like Nano or Notepad,
especially to start out. It's usually easier to move to more
complicated things when you are sufficiently frustrated with the
simple solution. Just make sure you have a way to create and edit text
files. As a final note, both Vim and Emacs have tutorials, so if you
choose Vim try typing `vimtutor` in your terminal, and if you choose
Emacs, just go through the tutorial it shows when you first open it or
type Ctrl+h followed by t.

## Your first program

Now that you have some editor, open a new file called `hello.py`. As
is tradition, our first program will simply print "Hello, World!" to
the screen. In Python this is very simple, just type

```python
print("Hello, World!")
```

into your editor and save it. Depending on your editor, there may be
some built-in ways to run the program, but I will not assume anything
about your editor. As such, go back to your terminal and type `python
hello.py`, making sure you are in the same directory as your
`hello.py` file. This should run the program and print the expected
message to your screen. Remember to type `python3 hello.py` instead if
your version check indicated that you needed to earlier. If this
worked, you should be ready to move on to the rest of the projects!
