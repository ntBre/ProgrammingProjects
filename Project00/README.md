# Setting up your programming environment

The purpose of this project is to get you ready to write code. This includes
having a reasonable version of Rust installed and knowing how to edit and run
your Rust files.

## Installing Rust

[This page](https://www.rust-lang.org/tools/install) explains how to install
Rust, but the recommended way to do it is simply to run the following command at
the command line:

``` shell
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

This will download an installation script from the Rust website and execute it
in your shell to download and install `rustup`, a tool for managing the rest of
your Rust installation. To double-check your installation, run one (or both) of
the following commands:

``` shell
cargo --version
rustc --version
```

On my machine running (an outdated version of) nightly Rust, the output of these
commands is

``` shell
cargo 1.72.0-nightly (5b377cece 2023-06-30)
rustc 1.72.0-nightly (839e9a6e1 2023-07-02)
```

As long as you get actual output and not something like `command not found`, you
should be good to go.

## Choosing an Editor

Now that you have Rust installed, you need a way to edit Rust files, which
typically end with the extension `.rs`. You can use any editor that can edit
plain text files, but a few suggestions are [Vim](https://www.vim.org/),
[Emacs](https://www.gnu.org/software/emacs/), and
[VSCode](https://code.visualstudio.com/). Of these, VSCode will be the easiest
to get started with, probably followed by Emacs and then Vim. Emacs has a better
graphical interface than Vim, but it is also more complicated and consequently
could be harder to use. Vim is probably the most confusing initially, but as the
simplest editor you may be able to use it quickly. It will also be installed by
default on Mac, Linux, and WSL. I use Emacs with Vim editing keybindings and
would recommend that to everyone, but it would take an entire project on its own
to get that set up. If you're interested, see my [recent
video](https://youtu.be/ecXhHc32XPU?t=4246) on setting up Emacs 29 for Rust
development. You can also use more basic editors like Nano or Notepad,
especially to start out. It's usually easier to move to more complicated things
when you are sufficiently frustrated with the simple solution. Just make sure
you have a way to create and edit text files. As a final note, both Vim and
Emacs have tutorials, so if you choose Vim try typing `vimtutor` in your
terminal, and if you choose Emacs, just go through the tutorial it shows when
you first open it or type `Ctrl+h` followed by `t`.

## Your first program

Now that you have some editor ready, use the `cargo` tool that comes with your
Rust installation to generate your first project:

``` shell
cargo new name-of-project
```

where `name-of-project` is a name of your choice.

As is tradition, our first program will simply print "Hello, World!" to the
screen. However, `cargo` has already prepared this example for us, so you can
run

``` shell
cargo run
```

at your command line to run the program (assuming you've changed to the project
directory). To see what code `cargo` generated, open `src/main.rs` in your text
editor. It should look like

``` rust
fn main() {
    println!("Hello, world!");
}
```

 If this worked, you should be ready to move on to the rest of the projects!
