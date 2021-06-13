# Molecular-Geometry-Analysis

The purpose of this project is to introduce you to fundamental Python
programming techniques in the context of a scientific problem, namely
the calculation of the internal coordinates (bond lengths, bond
angles, dihedral angles), moments of inertia, and rotational constants
of a polyatomic molecule.

#### Key concepts
[Opening files](#open)  
[For loops and range](#for)  
[Lists](#lists)  
[Conditionals and booleans](#cond)  
[With statement](#with)  

## Part 1: Read the Coordinate Data from Input

The input to the program is the set of Cartesian coordinates of the
atoms (in bohr) and their associated atomic numbers. A sample molecule
(acetaldehyde) to use as input to the program is:

```
7
6  0.000000000000     0.000000000000     0.000000000000
6  0.000000000000     0.000000000000     2.845112131228
8  1.899115961744     0.000000000000     4.139062527233
1 -1.894048308506     0.000000000000     3.747688672216
1  1.942500819960     0.000000000000    -0.701145981971
1 -1.007295466862    -1.669971842687    -0.705916966833
1 -1.007295466862     1.669971842687    -0.705916966833
```
    
The first line is the number of atoms, while the remaining lines
contain the Z-values (atomic charge) and x-, y-, and z-coordinates of
each atom. This [input file](./input/acetaldehyde.dat) and the other
test cases can be found in this repository in the [input
directory](./input).

Assuming you didn't clone the repository, download the input and
output directories in the form of a
[tar](https://en.wikipedia.org/wiki/Tar_(computing)) archive using the command

```
curl -O 'https://raw.githubusercontent.com/ntBre/ProgrammingProjects/master/Project01/files.tar'
```

you can then extract the files using the command

```
tar xvf files.tar
```

You can also copy and paste the files manually from GitHub, but the
`tar` approach will be more convenient when the number of files
increases in later projects.

After somehow getting the files to your computer, you must a) open the
file, b) read the data from each line into appropriate variables, and
c) finally close the file. This sounds pretty straightforward, but it
will introduce us to some important programming constructs. If you
know some Python, give this a shot on your own. Otherwise, expand the
code snippets below and type them into your editor of choice. It may
be tempting to copy and paste, but writing them out by hand will
better help you remember them in the future. We'll break the task into
the steps described above.

### a) Open the file

<details>

<summary>Tutorial</summary>

The basic way to open a file in Python is to use the 'open' function
as shown below.

<a id="open"/>

```python
infile = open("input/acetaldehyde.dat", "r")
```

The first argument is the name of the file we want to open, in this
case, "acetaldehyde.dat" in our "input" directory. The second argument
is a character describing how we want to open the file. In this case,
we use an "r" to stand for "reading" since we just want to read the
file. if instead we wanted to write a file, this second argument would
be "w".

The open function returns a "file object", the details of which are
not particularly important for now. What is important is what happens
to that file object after we call open. If we were to run only the
right portion of the line above, `open("input/acetaldehyde.dat",
"r")`, our file would disappear and we couldn't do anything useful
with it. Instead, we use the `=` **operator** to **assign** the file
object to a **variable**. We can then refer to the file object later
in our program by using this variable, `infile`, which is short for
input file.

If you want, you can try printing the file object using

```python
print(infile)
```

but this will not be very helpful since Python will just print a
fairly useless representation of a file object.

</details>

<details>

<summary>Solution</summary>

```python
infile = open("input/acetaldehyde.dat", "r")
```

</details>

### b) Read the data

<details>

<summary>Tutorial</summary>

The first thing I usually do when opening a file is just write a
simple **loop** to print all of the lines in the file. Loops, as the
name suggests, are a way to repeat an action. As a simple example, we
can use the Python `for` loop along with the `range` built-in to loop
5 times and print the number each time.

<a id="for"/>

```python
for i in range(5):
	print(i)
```

Each time through the loop, the variable `i` will be bound to a value
from 0 to 4. This is a bit tricky at first since you might think the
loop would run from 1 to 5, but since arrays, or Python's version
**lists**, which we will meet shortly, are indexed starting from 0,
this is actually convenient if unintuitive.

Another convenient fact is that Python file objects are iterable. This
means you can actually loop over a file directly as shown below.

```python
for line in infile:
	print(line)
```

The choice of name for the variable `line` is arbitrary although
convenient since we are in fact looping over the lines in the file. If
you run this code, you will notice that there are extra blank lines
between each line. This is because Python's default `print` function
tacks on a newline ('\\n') character to every line of output. To turn
this off, we can pass the **optional argument**, `end` to the `print`
function with a value of an empty **string**, giving us

```python
for line in infile:
	print(line, end="")
```

and some nicer output. This brings us to our first mention of **data
types**. Python does not place a great emphasis on different types of
data like some languages do, but the different types still exist and
they have different characteristics. Strings, for example, are
sequences of characters between quotes. We saw a string with our Hello
World example, although we did not name it as such. Python refers to
strings by the abbreviation `str`. Other types of data we will see in
this project are integers, which are whole numbers without decimal
parts, such as 1 or 2 or 123456, and floating point numbers, which are
numbers with decimal parts like 1.0 or 3.14. Python refers to these as
`int`s and `float`s, respectively.

Something else to note here is a very important aspect of
Python. Indentation matters, and it matters a lot. Instead of using
braces to indicate code blocks that are nested inside each other like
many other languages, Python uses indentation. If you wrote

```python
# NOTE: WRONG!
for line in infile:
print(line)
```

instead of the correct version we wrote above, you will get an error
telling you it expected an indented block. More dangerously, if we had
more than one line that was supposed to be inside the loop, as we will
later, and you only indented the first line, only that line would be
printed in the loop. For example,

```python
for line in infile:
	print("Hello")
print(line)
```

will print the string "Hello" 8 times, followed by the last line of
the file. Python is also very picky about the type of indentation you
use. Tabs vs spaces is a so-called "holy war" of computing, much like
Vim vs Emacs, so I won't tell you which to use. Just pick one and
stick with it or Python will be very angry with you. A good editor
will handle the indentation for you, so you may not even know which
you are using.

Now that you can loop over the lines of the file, we can start trying
to save the information in the file into a form we can use later. If
you have some experience programming, you might want to define an Atom
or Molecule class with charge, x, y, and z fields, but we will stick
with more basic **data structures** for now.

<a id="lists"/>

There are two data structures that we can use here. The first is the
most commonly-used way to collect multiple things into one, the
**list**. Lists in Python are written between brackets with
**elements** separated by commas like `[1, 2, 3]`. This is a list of
three elements, the integers 1, 2, and 3. You can assign a list to a
variable like we did with the file:

```python
l = [1, 2, 3]
```

will bind our list to the variable `l` so we can use it later. You can
grab individual elements of a list by **indexing** into it using
square brackets like `l[0]`, which will give you the zeroth element in
the list. Similarly, `l[1]` will give you the first element, and
`l[2]` will give you the second. `l[3]` will give you an error for
trying to reach an element that doesn't exist.

Loops and lists are intimately connected, and you can loop over a list
just like we did with our file using a for loop:

```python
for i in l:
	print(i)
```

This will print each element in our list. Note that this is different
from looping over the *indices* in the list, which would be 0, 1, and
2, not 1, 2, and 3. If you need both the indices and the elements at
those indices, you can either range over the **length** of the list,
using the built-in `len` function like

```python
for i in range(len(l)):
	print(i, l[i])
```

in which case you have to use `l[i]` to access the element of the
list, or you can use the `enumerate` keyword to get both at once.

```python
for i, v in enumerate(l):
	print(i, v)
```

This binds `i` to the index and `v` to the element or value at index
`i`.

Lists can also contain other lists, which we will take advantage of
shortly. For example,

```python
l = [6, [0.0, 0.0, 0.0]]
```

is a list of two elements, where the first is an integer, 6, and the
second element is itself a list containing three floating point zeros.

With that background on lists in mind, we should be ready to read and
store our atoms from the file. Since we have an open file object from
the previous step, we can start by looping over it:

```python
for line in infile:
```

Inside the loop, we probably need to **split** the line so we can
access the individual fields. We can do this with the aptly named
`split` **method**. For the sake of these projects, method and
function can be used basically interchangeably, but methods are
technically functions associated with a particular class of
object. `split` is a built-in string method, which means it acts on a
string. "Acting on" takes the form of `thing.action()` in the case of
methods, instead of functions which just look like `action()`. As an
example, contrast the `split` example below with the way we called the
`print` and `enumerate` functions.

```python
for line in infile:
	sp = line.split()
```

Now that we have split the line, we can print it to see what it looks like

```python
for line in infile:
	sp = line.split()
	print(sp)
```

The quotes around the elements in the printed results mean that all of
the elements are currently strings, so we're going to need to convert
them to integers and floats, respectively since we want to do math on
them eventually. You'll also see that the first line, which needs to
be treated a bit differently from the others, is also being printed.

<a id="cond"/>

When you need to make a decision in the code, you use what is called a
**conditional**. Python's conditional statement is called an `if`
statement. It lets you evaluate a set of expressions only *if* some
other expression is true. For example,

```python
if 2 > 1:
	print("2 is greater than 1")
```

will print the given message if 2 is in fact greater than 1. This type
of numerical **comparison** is obviously not particularly interesting
since it will always be true or false. However, it is useful for
demonstrating both the comparison operators and introducing another
data type, the **boolean**. The comparison operators should be pretty
familiar from algebra, but they are listed in the table below.

| Operator | Definition            |
|----------|-----------------------|
| >        | Greater than          |
| <        | Less than             |
| >=       | Greater than or equal |
| <=       | Less than or equal    |
| ==       | Equal                 |
| !=       | Not equal             |

Booleans are similarly straightforward as they only have two possible
values, true or false, which are written as `True` and `False` in
Python. Boolean expressions that are true evaluate to `True` and those
that are false evaluate to `False`. 2 > 1 in the example above
evaluates to `True`, so it is equivalent to writing `if True:`.

For our purposes, we want to check if the length of our split line is
equal to 4, that is it contains a Z value and 3 Cartesian
coordinates. We can do that with

```python
if len(sp) == 4:
	print(sp)
```

and combining that with our loop from earlier gives

```python
for line in infile:
	sp = line.split()
	if len(sp) == 4:
		print(sp)
```

Note how the indentation increases with each new block we
introduce. If you run this code, you should notice that the number of
atoms line is no longer printed. That line is useful in some (old)
languages where it is not as easy to write "loop until the end of the
file" as in Python, but we don't need it. Another way we could have
gotten rid of it is by counting the number of lines we have read and
skipping the first one, but this solution has the added benefit of
skipping blank lines that can sometimes be accidentally introduced
especially at the end of the file.

The next thing we should do is convert our values to the right
type. We probably want our Z values to be integers, and we definitely
want our x, y, and z coordinates to be floats. We can make that change
using the code below, where you can use the Python type names I
mentioned earlier as functions to convert values to that type.

```python
for line in infile:
	sp = line.split()
	if len(sp) == 4:
		t = [int(sp[0]), float(sp[1]), float(sp[2]), float(sp[3])]
		print(t)
```

Now there should not be any quotes around the values and they are
ready to do mathematical operations on later. The only thing left is
to actually save these lines for later use. We can put each of these
lists into another list to keep them together under one
variable. First we need to initialize an empty list outside our loop.

```python
atoms = []
```

`atoms` is a good name since these numbers represent the atomic charge
and coordinates of atoms. We make an empty list by writing brackets
with nothing inside them. Then we can **append** to the list, by using
the again aptly named `append` method of lists inside our loop.

```python
atoms = []
for line in infile:
	sp = line.split()
	if len(sp) == 4:
		t = [int(sp[0]), float(sp[1]), float(sp[2]), float(sp[3])]
		atoms.append(t)
print(atoms)
```

Running this, you can see that we now have all of our atoms in a list
called `atoms`. `append` just adds a new element, in our case `t`, to
the end of a list, turning our initially empty list into a full list
of atoms.

</details>

### c) Close the file

<details>

<summary>Tutorial</summary>

There's not going to be much difference between the Tutorial and
Solution in this case. The only small difference between opening and
closing the file is that `open` was a built-in function, while `close`
is a file method. As such, instead of writing `close(infile)`, you
just write

```python
infile.close()
```

</details>

<details>

<summary>Solution</summary>

```python
infile.close()
```

</details>

### d) Refactoring

<details>

<summary>Tutorial</summary>

<a id="with"/>

Refactoring is what you call it when you restructure existing code
without affecting its functionality. Instead of having separate steps
for opening and closing the files, Python has a useful construct for
this exact scenario called the `with` construct. Below is the current
version of the code with the separate open and close

```python
infile = open("input/acetaldehyde.dat", "r")
atoms = []
for line in infile:
	sp = line.split()
	if len(sp) == 4:
		t = [int(sp[0]), float(sp[1]), float(sp[2]), float(sp[3])]
		atoms.append(t)
print(atoms)
infile.close()
```

and here is what it looks like with a `with` statement

```python
atoms = []
with open("input/acetaldehyde.dat", "r") as infile:
	for line in infile:
		sp = line.split()
		if len(sp) == 4:
			t = [int(sp[0]), float(sp[1]), float(sp[2]), float(sp[3])]
			atoms.append(t)
print(atoms)
```

In addition to saving two lines of code, this prevents you from
forgetting to close the file when you finish and also ensures the file
is closed even if some kind of error or exception occurs between the
open and close. This is not that important for our current use case
since our programs are very short-lived, but if your program runs for
a long time and opens many files without closing them, the operating
system can even stop you from opening more.

Another nice thing we could do is refactor our code into a function. I
have mentioned functions before as built-in features of the language
that do handy things. We can also define our own functions, which
allows us to reuse pieces of code. You can think of functions like
functions in math class, basically serving to convert something into
something else. For example, the mathematical function `f(x) = 2x`
takes a single argument, `x` and returns that argument multiplied by
the number 2. We can write the same function in Python like

```python
def f(x):
	return 2*x
```

Here you can see that we have to use the `def` keyword instead of a
simple equals sign since the equals sign already handles variable
assignment in Python. We also have to explicitly write `return` to
actually send a value back out of our function.

In the case of our current project, our input argument will probably
be the filename, and the output we return will be a list of
atoms. This will allow our code to be reused for the different test
cases without having to change the filename directly in our `open`
call.

To start, we can just sandwich our current code in between a `def` and
a return, giving it the name `load_atoms`. In addition to being named
after a snake, the naming convention in Python is to use lowercase
function names with words separated by underscores, also known as
snake case. You don't have to follow this, but I will just to be
Pythonic.

```python
def load_atoms():
	atoms = []
	with open("input/acetaldehyde.dat", "r") as infile:
		for line in infile:
			sp = line.split()
			if len(sp) == 4:
				t = [int(sp[0]), float(sp[1]), float(sp[2]), float(sp[3])]
				atoms.append(t)
	print(atoms)
	return
```

This version doesn't give us much improvement, but you can achieve the
same behavior as before by adding a call to the function like

```python
load_atoms()
```

below the definition. To complete our refactor, let's make
`load_atoms` actually take the argument we mentioned above, and
instead of printing anything inside the function, we'll return our
list of atoms and let whoever wants to call it print the result if
they want. This gives us the code below.

```python
def load_atoms(filename):
	atoms = []
	with open(filename, "r") as infile:
		for line in infile:
			sp = line.split()
			if len(sp) == 4:
				t = [int(sp[0]), float(sp[1]), float(sp[2]), float(sp[3])]
				atoms.append(t)
	return atoms
	

print(load_atoms("input/acetaldehyde.dat"))
```

This may not strike you as much of an improvement, and it did add some
more lines to type, so it may even seem like a bad thing, but keep in
mind that you can now load the other two provided input files without
copying and pasting all your code. In the next subsection on testing,
we will see another benefit of organizing your code in this way.

</details>

## Step 2: Bond Lengths
Calculate the interatomic distances using the expression:

<img src="./figures/distances.png" height="40">

where x, y, and z are Cartesian coordinates and i and j denote atomic indices.

- [Hint 1](./hints/hint2-1.md): Memory allocation
- [Hint 2](./hints/hint2-2.md): Loop structure
- [Hint 3](./hints/hint2-3.md): Printing the results
- [Hint 4](./hints/hint2-4.md): Extending the Molecule class
- [Solution](./hints/step2-solution.md)

## Step 3: Bond Angles
Calculate all possible bond angles. For example, the angle, &phi;<sub>ijk</sub>, between atoms i-j-k, where j is the central atom is given by:

<img src="./figures/bond-angle.png" height="25">

where the e<sub>ij</sub> are unit vectors between the atoms, e.g.,

<img src="./figures/unit-vectors.png" height="30">

- [Hint 1](./hints/hint3-1.md): Memory allocation for the unit vectors
- [Hint 2](./hints/hint3-2.md): Avoiding a divide-by-zero
- [Hint 3](./hints/hint3-3.md): Memory allocation for the bond angles
- [Hint 4](./hints/hint3-4.md): Smart printing
- [Hint 5](./hints/hint3-5.md): Trigonometric functions
- [Solution](./hints/step3-solution.md)

## Step 4: Out-of-Plane Angles
Calculate all possible out-of-plane angles. For example, the angle &theta;<sub>ijkl</sub> for atom i out of the plane containing atoms j-k-l (with k as the central atom, connected to i) is given by:

<img src="./figures/oop-angle.png" height="60">

- [Hint 1](./hints/hint4-1.md): Memory allocation?
- [Hint 2](./hints/hint4-2.md): Cross products
- [Hint 3](./hints/hint4-3.md): Numerical precision
- [Hint 4](./hints/hint4-4.md): Smarter printing
- [Solution](./hints/step4-solution.md)

## Step 5: Torsion/Dihedral Angles
Calculate all possible torsional angles. For example, the torsional angle &tau;<sub>ijkl</sub> for the atom connectivity i-j-k-l is given by:

<img src="./figures/torsion-angle.png" height="60">

Can you also determine the sign of the torsional angle?

- [Hint 1](./hints/hint5-1.md): Memory allocation?
- [Hint 2](./hints/hint5-2.md): Numerical precision
- [Hint 3](./hints/hint5-3.md): Smart printing
- [Hint 4](./hints/hint5-4.md): Sign
- [Solution](./hints/step5-solution.md)

## Step 6: Center-of-Mass Translation
Find the center of mass of the molecule:

<img src="./figures/center-of-mass.png" width="600">

where m<sub>i</sub> is the mass of atom i and the summation runs over all atoms in the molecule.

Translate the input coordinates of the molecule to the center-of-mass.

- [Hint 1](./hints/hint6-1.md): Atomic masses
- [Hint 2](./hints/hint6-2.md): Translating between atomic number and atomic mass
- [Solution](./hints/step6-solution.md)

## Step 7: Principal Moments of Inertia
Calculate elements of the [moment of inertia tensor](http://en.wikipedia.org/wiki/Moment_of_inertia_tensor).

Diagonal:

<img src="./figures/inertia-diag.png" width="750">

Off-diagonal (add a negative sign):

<img src="./figures/inertia-off-diag.png" width="600">

Diagonalize the inertia tensor to obtain the principal moments of inertia:

<img src="./figures/principal-mom-of-inertia.png" width="125">

Report the moments of inertia in amu bohr<sup>2</sup>, amu &#8491;<sup>2</sup>, and g cm<sup>2</sup>.

Based on the relative values of the principal moments, determine the [molecular rotor type](http://en.wikipedia.org/wiki/Rotational_spectroscopy): linear, oblate, prolate, asymmetric.

- [Hint 1](./hints/hint7-1.md): Diagonalization of a 3×3 matrix
- [Hint 2](./hints/hint7-2.md): Physical constants
- [Solution](./hints/step7-solution.md)

## Step 8: Rotational Constants
Compute the rotational constants in cm<sup>-1</sup> and MHz:

<img src="./figures/rot-const.png" width="100">

- [Solution](./hints/step8-solution.md)


## Test Cases
- Acetaldehyde: [input coordinates](./input/acetaldehyde.dat) | [output](./output/acetaldehyde_out.txt)
- Benzene: [input coordinates](./input/benzene.dat) | [output](./output/benzene_out.txt)
- Allene: [input coordinates](./input/allene.dat) | [output](./output/allene_out.txt)

## References
E.B. Wilson, J.C. Decius, and P.C. Cross, __Molecular Vibrations__, McGraw-Hill, 1955.
