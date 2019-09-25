
## Subroutines and modules

We can now write fairly large programs. As they get larger and longer, they get
harder to understand, harder to keep track of what they’re doing, and harder to
make changes when changes are necessary.

There are several ways you’ll see this effect in your actual code. First, code will
get repetitive; you’ll find yourself repeating whole blocks of code in your programs.
This is always a bad idea. The problem is that if you ever need to change one of
these blocks, you’ll typically need to change all of them, and it’s quite easy to either
forget to do that, or do be inconsistent about it.

Another way you’ll see this in a language like Python is that your indentation for
code blocks will become confusing. You’ll be working on some line of code at the
end of a block that’s tabbed/spaced in some number of times and not being sure
how many tabs or spaces you need for the next line.

These issues make us want to factor our code, break it into more efficient and conceptually
more reasonable chunks: functions and modules.

#### Simple functions

Functions are defined with the `def` keyword, followed by a function name of your
choosing, parentheses, and colon. These are followed by a block of statements.


```python
def myfunction():
    print('This is a function')
    print("That's all it does")
```

We can invoke this function just as we invoke any other function. The invocation
must follow the function defintion (but need not follow it immediately of course).


```python
def myfunction():
    print('This is a function')
    print("That's all it does")
#invoking that function
myfunction()
```

    This is a function
    That's all it does
    

Functions allow us to simplify repetitive code. Consider the following simple program:


```python
#print a famous sentence over two lines
print('Colorless green ideas...')
print('...sleep furiously')
#get the user to enter a number
num = input('Enter a number: ')
#print the sentence again if it’s < 5
if int(num) < 5:
    print('Colorless green ideas...')
    print('...sleep furiously')
else:
    print('Your number was big enough')
```

    Colorless green ideas...
    ...sleep furiously
    Enter a number: 6
    Your number was big enough
    

Notice how the first and second lines are completed in the `if` block. We can avoid
this repetition by defining our own function:


```python
#print a famous sentence over two lines
def myfunc():
    print('Colorless green ideas...')
    print('...sleep furiously')
#invoke the function
myfunc()
#get the user to enter a number
num = input('Enter a number: ')
#print the sentence again if it’s < 5
if int(num) < 5:
    myfunc()
else:
    print('Your number was big enough')
```

    Colorless green ideas...
    ...sleep furiously
    Enter a number: 3
    Colorless green ideas...
    ...sleep furiously
    

Here we factor out the repeated two-line section as a separate function. We then
call that function twice in the following code. 
The new code 

+ makes clear that those repeated parts are the same
+ is also easier to maintain in the sense that if we wanted to change one of the repeated
lines, we can do so once and the change is applied in both applications of the
function

Functions can be more complex of course. Here’s a slightly longer bit of code that
takes input from the user.


```python
#a function
def myfunc():
    #user supplies a word
    word = input('Word: ')
    #print that word
    print('This is your word: ',word)
    #check if > 5
    if len(word) > 5:
        print('Your word was long.')
    else:
        print('Your word was short.')
#invoke the function
myfunc()
```

    Word: elephant
    This is your word:  elephant
    Your word was long.
    

Here the function reads user input, prints it, and then does different things depending
on the length of the input.
Notice how the function code creates a variable `word`. It’s important to note that
that variable is available only **inside** the function. If we try to refer to a variable created
and assigned a value inside some function outside that function, we get an error.
Here’s an example of that:


```python
#this doesn’t work!
def myfunc():
    word = input('Word: ')
    print('This is your word:',word)
myfunc()
if len(word) < 5:
    print("Your word wasn't long enough")
```

    Word: linguist
    This is your word: linguist
    


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-2-f2100897c4c3> in <module>()
          4     print('This is your word:',word)
          5 myfunc()
    ----> 6 if len(word) < 5:
          7     print("Your word wasn't long enough")
    

    NameError: name 'word' is not defined


On the other hand, variables outside a function are available inside a function.
Here’s an example:


```python
#user supplies a word
word = input('Word: ')
#function refers to previous value!
def myfunc():
    print('This is your word: ',word)
#invoke the function
myfunc()
#check if the word is less than 5 letters
if len(word) < 5:
    print("Your word wasn't long enough")
```

    Word: linguist
    This is your word:  linguist
    

Here the value of `word` is set outside the function. When the function is called, it
has access to that value.

#### Functions that return values

So far, our functions have taken no arguments and have returned no values. In
this section, we will see how to write functions that return a value. The syntax is very
simple, the returned value of a function follows the keyword `return`. Here’s a
simple example:


```python
#function definition
def myfunc():
    #prints this
    print("This prints.")
    #return the value 6
    return 6
    #gratuitous print command
    print("This doesn't print!")
#invoke the function, assign value to x
x = myfunc()
#print the value of x
print("Here's the function output:",x)   
```

    This prints.
    Here's the function output: 6
    

Notice how the first `print` statement executes, but the second does not. The
`return` statement exits the function, so subsequent statements cannot run.

This does not mean that `return` must always be last in the function. We can, for
example, embed `return` in an `if` structure.


```python
#function definition
def lcountfunc():
    #user supplies a word
    wd = input('Type a word: ')
    #check the length of the word
    if len(wd) > 4:
        #return length of word...
        #...and exit function
        return len(wd)
    #otherwise...
    else:
        print('The word is too short!')
#save value of function in variable
res = lcountfunc()
#print value of variable
print('The result: ',res)
```

    Type a word: linguist
    The result:  8
    

Note that this function either returns a value or prints a value. If you use it in a context where you expect it to return a value, with `=` for example, we end up with
the non-value `None` if it does not, in fact, return a value.

Functions can also return more than one value. This is as simple as putting several
values—seperated by commas—after the `return`. Here’s a simple example:


```python
#function definition
def myfunc():
    #collect two strings
    x = input('First string: ')
    y = input('Second string: ')
    #concatenate the strings
    z = x + ' ' + y
    #return all three
    return len(x),len(y),z
#invoke the function saving all
#3 return values
a,b,c = myfunc()
#print the three values
print('a =',a)
print('b =',b)
print('c =',c)
```

    First string: happy
    Second string: linguist
    a = 5
    b = 8
    c = happy linguist
    

Here the function prompts for two strings and then returns three values: the length
of the first string, length of the second string, and the concatenation of the two
strings. Note incidentally that the returned values need not be of the same type.
Here, the first two returned values are integers and the third is a string.

#### Functions that take arguments

Functions can take arguments as well. This is superficially simple to do, but can
get tricky. Basically, for a function to take an argument, you put some number of
variable names in the parentheses in the function definition. Here’s a very simple
example:


```python
#function that takes 2 arguments
def myfunc(a,b):
    #return the concatenation
    #OR addition of those values
    return a + b
#invoke the function with numbers
print(myfunc(3,10))
#invoke the function with strings
print(myfunc('strings ','too'))
```

    13
    strings too
    

In this example, we give our function two arguments `a` and `b`. The function then
applies the `+` operator to those. If we invoke the function with integer arguments,
the result is the addition of the arguments. If we invoke the function with string
arguments, we get the concatenation of those arguments. Thus Python does not
generally restrict the type of the arguments a function can take.

Ideally, argument names should be novel, not to be confused with other variables.
Let’s consider this a bit more closely however. Compare the following two programs:


```python
x = 'a value'
def anotherfunc(a):
    a = 'another value!'
    return a
print(x)
print(anotherfunc(x))
print(x)
```

    a value
    another value!
    a value
    


```python
x = [4,5,6]
def anotherfunc(a):
    a.append(7)
    return a
print(x)
print(anotherfunc(x))
print(x)
```

    [4, 5, 6]
    [4, 5, 6, 7]
    [4, 5, 6, 7]
    

The difference between these two programs corresponds to mutability. Mutable
objects all work as in the second program; immutable objects work as in the first
one.

We’ve already seen functions with more than one argument. There is more than
one way to invoke these. Consider this example:


```python
#function definition
def thefunction(x,y):
    return x + ' ' + y
#invoke the function 3 ways
print(thefunction('one','way'))
print(thefunction(x = 'another',y = 'way'))
print(thefunction(y = 'way',x = 'yet another'))
```

    one way
    another way
    yet another way
    

Here we define a function with two arguments and invoke it three different ways.
One way is to just provide two arguments; these are interpreted as the two arguments
in the function in the same order. A second way, is to name the variables.
The names tell us which argument gets associated with which variable. Note that if we take this option, we can give the names in any order, as above.

The `=` can be used in the function declaration as well to give default values to the
function arguments. Here’s an example:


```python
#function with default value
#for 2nd argument
def f(x,y = 'oops'):
    return x + ' ' + y
#invoked 3 ways
print(f('hat'))
print(f(x='chair'))
print(f('hat','chair'))
```

    hat oops
    chair oops
    hat chair
    

Note that if you mix arguments with and without default values in your function
declaration, all the arguments with default values must follow the arguments without.

You can also write functions with a variable number of arguments. If you want
a variable number of unnamed arguments, you put some variable name in the
parentheses in your function declaration with a preceding asterisk. This variable
can then be used as a list in the function body. If you want a variable number of
named arguments, you put some variable name in the parentheses in your function
declaration with two preceding asterisks. This variable can be used as a dictionary in the function body. If you use both, the list variable must precede the dictionary
variable. Here is a simple example:


```python
#function with an unspecified
#number of unnamed and named arguments
def func(*args,**kwargs):
    #print unnamed args
    for a in args:
        print('\t',a)
    #print named args
    for k in kwargs:
        print('\t',k,'\t',kwargs[k])
#invoked with unnamed FOLLOWED by
#named arguments
func(3,6,8,hat='wow',chair=3.5)
```

    	 3
    	 6
    	 8
    	 hat 	 wow
    	 chair 	 3.5
    

This function simply prints out all variables given as unnamed variables and then
prints out all variables given as named variables. The latter are printed with their
names.

#### Modules

You can import pre-written code as a module, e.g.,

```
import re
import random
from sys import ardv #to import only specific elements of a module 
import sys as s #to create an alias for the module
```
