
# Python. Basic functions.

When you install Python, you can choose among different versions. We will be using any of the 3.x versions.

There are at least three ways you can invoke Python:
1. interactive environment terminal or Python window
2. idle Python integrated development environment
3. edit & run write a program that you run in the terminal window
4. jupyter notebooks write code that runs interactively in a web browser

We start by playing with the interactive environment. 

If Python is on your system you can start the
interactive environment by simply typing python in the terminal window on a
Mac or choosing Python from the start menu on Windows. This will produce this
response:

```
$ python
Python 3.7.0 ...
Type ”help”, ”copyright”, ”credits” or
”license” for more information.
>>>
```

The version of Python that you're using is displayed along with additional system
information. All of this is followed by the prompt `>>>`. Your commands are typed
at that prompt.

Before going any further, let's set out the most most important commands that work
here:
1. `Quit: quit()`. Type this at the `>>>` prompt to exit the interactive environment.
Typing `^d (control-d)` has the same effect.
2. `Help: help()`. Typing this enters the on-line help system where you can get help
on many aspects of using Python. While this is extremely helpful, the responses it
provides may not be terribly useful at this stage. You exit this system and return to
the interactive environment with the return key.
3. `Interrupt: ^c (control-c)`. When we start playing with the system, you will
occasionally get stuck in the middle of a command or while some command is
running. If you do get stuck, if some command seems to be running forever, you
can often regain control and return to the `>>>` prompt by typing `^c`.

In the interactive environment, you can type Python
statements and they are immediately evaluated. For example, you can perform
mathematical calculations like multiplication or addition:
```
>>> 3 * 8
24
>>> 6 + 4.7
10.7
>>> 5 - 10
-5
```

Words and sentences (character strings) must be
entered in single or double quotes. 
```
’This is a sentence’
”This is another one”
```
Interestingly, some of the mathematical operators above can be used with character
strings. With numbers `+` is addition, but with
strings it is concatenation. With numbers `*` is multiplication, but with a string and a
number it repeats the string:
```
>>> ’phon’ + ’ology’
’phonology’
>>> ’phon’ * 7
’phonphonphonphonphonphonphon’
```


There are some functions that operate directly on strings. The `len()` function
returns the number of characters in a string.
```
>>> len(’semantics’)
9
```
The `type()` function can operate on strings or numbers and returns the general
“type” of the object it applies to.
```
>>> type(5)
<class ’int’>
>>> type(8.7)
<class ’float’>
>>> type(’Dasha’)
<class ’str’>
```
The quotes surrounding a character string are essential and distinguish
strings from other types. What happens, if you leave them out?

If you put quotes around numbers, you change the basic type of the object.
Consider the difference here:
```
>>> 8 + 3
11
>>> ’8’ + ’3’
’83’
```

There are functions for converting back and forth between character strings, integers,
and floating point numbers:
```
>>> int(’8’)
8
>>> float(’7.8’)
7.8
>>> str(7)
’7’
```
Operators and functions can be combined as well. For example:
```
>>> (7 + 4) * 2
22
>>> str(8) + str(5)
’85’
>>> int(str(7)) * 3
21
```

The format we've used for functions is to invoke the function by putting parentheses
after its name, e.g. `str()`. There are other functions with a different syntax -- methods, functions that are very
specifically associated with some particular datatype. To invoke one of these, the method name and parentheses
are suffixed to the relevant object with a period. For example, the string method
`upper()` returns an uppercase version of a string. We invoke it as follows:
```
>>> ’this is awesome’.upper()
’THIS IS AWESOME’
```
There are methods that take additional arguments as well. For example, count()
returns the number of instances of its argument in the string.
```
>>> ’this is awesome’.count(’i’)
2
```

Let's move on from the interactive environment and write a program 
```
print('hello!')
```
in a text editor (you can use IDLE to create a text file, Emacs (or Aquamacs)), save the file as `hello.py` and run it in the terminal/command line.

The simplest way to run a program is to type
`python hello.py` in the terminal or the command line:

```
> python hello.py
hello!
```
If you invoke the program as above, it’s important that the program be in the same
directory that the terminal window is in. To find out what directory you are in, you
can type `pwd` at the terminal prompt. To see if this program file is in that directory, you can use the `ls` command at the terminal prompt. If it is not, you can either
move it there or you can instruct the terminal to switch to another directory with
the `cd` command (followed by the path to the directory you want to be in).


Once can also add comments to a code file. Comments are lines of code that remind
the programmer of what the code does or should do. Comments are marked
with a `#` on their left. Everything on the same line after that `#` have no effect on
the program. Comments can occur on their own line or on the right side of an actual
line of code.

```
#the greeting
print('hello!')#change this line later
```

**Exercises:**
1. Write commands that print out your first name, the number of characters in
that name, your last name, the number of characters in that name, and then
concatenates and prints the two names (with a space).
2. What’s the difference between these?
```
str(3 + 3) + ’3’
int(’3’) + int(’3’ + ’3’)
```
3. What’s the difference between these?

```’This is Mike’.upper().lower()
’This is Mike’.lower().upper()
```
4. Why does ```upper(’This is a cat’)``` not work?
5. What does the mathematical operator `**` do?
6. In math, `6 + 2` and `2 + 6` mean the same thing. We’ve seen that `+` and `*`
can be used with strings too. What happens if arguments are reversed when
strings are involved? Do those expressions mean the same thing?
