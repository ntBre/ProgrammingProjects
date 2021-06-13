# Programming Tutorial in Chemistry

This is a fork of the [Crawford Programming
Projects](https://github.com/CrawfordGroup/ProgrammingProjects) that
seeks to place more emphasis on learning to program in Python. The
original projects are a great resource, but some of the instructions
can be a bit vague, and C++ itself is not the easiest language to
begin with. As such, this version will give fuller instructions for
the chemistry problems as well as embed more language information
directly in the tutorial. One of the difficulties of learning to
program is that the best way to learn is by working on a concrete
project. The goal of this tutorial then is to offer a substantial,
quantum chemistry-flavored project to help people learn Python and
maybe a few basics of the shell.

# Getting Started

This repository is organized into several projects, each with its own
directory. In each one you will find a `README.md` file like this one
with instructions and output for you to check your implementation
against. These projects will also require some input files that will
be discussed in each project as they become relevant.  These input
files can be found in the `input` directory. Within `input` there are
directories for several different molecule/basis-set combinations
where you will find integrals, molecular geometries and other files to
use as input to your programs. There is also a tarball of the inputs
and outputs in each project directory to make it more convenient to
download all of the files you need. At least this is the case in the
Projects I have at least started working on. If you don't see a .tar
file and you want the updated Python version of the project, you
probably need to wait. Downloading and extracting these is covered in
[Project 1](Project01/README.md). Before Project 1 is [Project
0](Project00/README.md), which will help you get set up to write and
run Python programs. If you already know how to do that, skip ahead to
Project 1.

# Typographical Conventions

Following the conventions of many other programming tutorials, code
snippets will be written in `monospace` font, while new keywords will
be presented in **bold**. Part of being a good programmer is knowing
how to look for help on the internet and in documentation, so these
will try to help you know what terms to search for. There will also be
a Table of Contents below the Summary of each project providing quick
links to the important concepts introduced in that project to make it
easier to refer to them later. Commands that should be typed at a
shell in a terminal are prefaced with a `$`, such as `$ pwd`.

Code snippets are divided into two types: Tutorial and Solution. As
you might guess, the Tutorial blocks include full explanations of the
code and build up to the final solutions, introducing new concepts as
needed. In contrast, the Solution blocks only include the code
required to get the desired output. If you are learning Python for the
first time, you will obviously want to read the Tutorials, but
programming experts (hopefully including the future selves of current
beginners!) may want to refer directly to the Solutions. New concepts
are primarily introduced in the early projects, so that is where most
of the tutorials are found. Similarly, the original versions of these
projects did not provide full solutions to later projects. In an
effort to keep these projects usable as class assignments, I have also
limited the full solutions to those in the original version.

The available solutions may not be the shortest or most efficient. I
usually like playing [code
golf](https://en.wikipedia.org/wiki/Code_golf) in Python, but for the
sake of teaching I have sought to write in a more verbose style,
including defining some unnecessary variables and avoiding list
comprehensions. If you know how to do something faster, please feel
free to do it that way. If an instructor one day chooses to use this
version of the projects and tries to grade your code based on
similarity to mine instead of on the correctness of the output, please
show them this sentence telling them not to.

# Quantum Chemistry Programming Projects 
 - [Project #0](Project00/README.md): Setting up your programming environment
 - [Project #1](Project01/README.md): Molecular Geometry/rotational constant analysis
 - [Project #2](Project02/README.md): Harmonic Vibrational analysis
 - [Project #3](Project03/README.md): The Hartree-Fock self-consistent field (SCF) procedure.
 - [Project #4](Project04/README.md): The second-order Moller-Plesset perturbation (MP2) energy.
 - [Project #5](Project05/README.md): The coupled cluster singles and doubles (CCSD) energy.
 - [Project #6](Project06/README.md): A perturbative triples correction to CCSD [CCSD(T)].
 - [Project #7](Project07/README.md): Connecting your code to PSI4.
 - [Project #8](Project08/README.md): DIIS extrapolation for the SCF procedure.
 - [Project #9](Project09/README.md): Using symmetry in the SCF procedure.
 - [Project #10](Project10/README.md): DIIS extrapolation for solving the CC amplitude equations.
 - [Project #11](Project11/README.md): An "out of core" SCF procedure.
 - [Project #12](Project12/README.md): Excited Electronic States: CIS and TDHF/RPA
 
# Possible Future Projects
 - Loading basis sets and computing integrals
