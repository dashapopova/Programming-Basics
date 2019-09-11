
# Datatypes and variables
Python datatypes and variables that we will discuss today:

+ Numbers: integers and floats
+ Strings
+ Lists
+ Tuples
+ Dictionaries

## Variable assignment

We take some value and put it in a named location or recepticle. The syntax is
simple: the name occurs on the left, the value on the right, and `=` goes in between.

```
>>> x = 17
>>> bananas = 3.4
```
Note that this is not the same thing as equality. We’re not asserting that `bananas`
and `7.7` are the same thing; we’re taking the value `7.7` and giving it the name
`bananas`. Once a variable name has been bound to a value, it can be used anywhere a value
of that type can be used. For example:

```
>>> 3 + x
20
>>> bananas * 7
23.8
```

Variable names must begin with a letter or an underline. The remainder of the
name can consist of any additional letters, underlines, or numbers. Variable names
are case-sensitive and you should not use any of the reserved Python words:

+ `False class finally is return`
+ `None continue for lambda try`
+ `True def from nonlocal while`
+ `and del global not with`
+ `as elif if or yield`
+ `assert else import pass`
+ `break except in raise`

The right side of an assignment can include functions and variables. For example:

```
>>> oranges = bananas * 4
>>> bananas = bananas - 5
```
Notice that the latter statement confirms that even though assignment uses the symbol `=`, it is not to be confused with some sort of equality test. To test for equality, use `==`:

```
>>> 2 + 2 == 4
True
>>> ’hats’ == ’hat’ + ’s’
True
```
The choice of variable name is extremely important. While in principle, we can name our variables in many different ways, what we should always do is name our variables so that the name of the variable reminds
us what kind of value we are storing in it. For example, if we had a variable that we
stored somebody’s age in, a very convenient name would be something like `age`.
Far less useful would be a name like `theNumber`. While it does imply that
the variable contains a number, it does nothing to help us remember what number
we have stored. 

## Data types

1. **Numbers**

For numbers, there are three basic types: integer, floating point, and complex.

+ type `integer` example `3` convert from string `int(’3’)`
+ type `float` example `7.2` convert from string `float(’7.2’)`
+ type `complex` example `2+4j` convert from string `complex(’2+4j’)`

All of these can be converted to a string with the `string()` function.

2. **Booleans**

There is also a basic datatype for booleans, expressions that are true or false. This
class includes only two basic members: `True` and `False`. It also includes the
basic logical operators: `and`, `or`, and `not`. We can construct simple logical expressions
with these:
```
>>> True and False
False
>>> not (False or False)
True
>>> not (not True)
True
```
Here and elsewhere, we use parentheses to make the scope of operations clear. The
following are not equivalent.
```
>>> not (False or True)
False
>>> (not False) or True
True
```
We can, of course, also assign boolean values to variables:
```
>>> x = True
>>> y = False
>>> x and y
False
>>> (y or (not y))
True
```
We can also do comparisons on other datatypes that result in boolean values. For example, we have the following numerical comparisons:
```
Comparison Example
equality 3 == 2 + 1
inequality 7 != 2
greater than 5 > 3
greater than or equal 5 >= 5
less than 2 < 7
less than or equal 5 + 6 <= 10 * 3
```
We can build up fairly complex expressions now. For example:
```
>>> len(’hat’) > 7 - 2 or 7 - 2 == 3
False
>>> True and (8 = 4 + 4) and (True or False)
True
```
We’ve already seen that the `type()` function returns the type of an element. For
example:
```
>>> type(3)
<class ’int’>
>>> type(’3’)
<class ’str’>
```
There is a boolean version of this as well `isinstance()` that we can use to test
if some element or variable is of any particular type. For example:
```
>>> isinstance(3,int)
True
>>> isinstance(3.0,float)
True
>>> isinstance(’hat’,str)
True
>>> isinstance(3 == 4,bool)
True
>>> isinstance(3 + 4j,complex)
True
```
3. **Strings**

For linguists, strings are an extremely important datatype. As linguists, we are
often concerned with sounds, words, and sentences, and these are typically most
naturally represented as strings of characters.
Simple
strings are marked with single or double quotes. They are interchangeable:
```
>>> ’hat’ == ”hat”
True
```
Triple quotes allow a string to continue over multiple lines.
```
’’’This is a string
that continues on
more than one line’’’
```
You can use double quotes as well:
```
”””This is a string
that continues on
more than one line”””
```
If you assign such a string to a variable and then type the variable name, it looks
like a single line:
```
>>> x = ’’’This is
more
than one line’’’
>>> x
’this is\nmore\nthan one line’
```
The character
`\n` represents a line break and will display as such when the variable is explicitly
printed:
```
>>> print(x)
This is
more
than one line
```
In fact, one can use single or double quotes to specify a multi-line string if one
enters `\n` directly:
```
>>> y =’this is more\nthan one\nline too’
>>> print(y)
this is more
than one
line too
```
Thus the way to think about triple-quoted strings is not that they are a different
kind of string, but a convenient way to enter multi-line strings.
A similar issue arises with other special characters, e.g. tab. One cannot enter the
tab character directly in either of the string types we’ve discussed in the interactive
environment. Instead, a tab can be typed into either type of string as `\t`. Notice
how the tab is not displayed properly when the name of the variable is typed, but
only when the variable is given as an argument to `print()`.
```
>>> x = ’a\tfew\ttabs\there’
>>> x
’a\tfew\ttabs\there’
>>> print(x)
a few tabs here
```
What if you actually want
to type a backslash followed by a t or an n? With a single-, double-, or triplequoted
string, you have to enter a double backslash `\\`. If you assign the string to
a variable name and then type that name, you see the double slash; if you invoke
the variable with `print()`, then only a single slash is displayed:
```
>>> x = ’xyz\\nabc’
>>> x
’xyz\\nabc’
>>> print(x)
xyz\nabc
```
If you’re entering strings with lots of special characters that require backslashes, this
is where the raw string notation becomes useful. If you prefix a single- or doublequoted
string with r, then backslash is interpreted as a backslash.
```
>>> x = r’abc\nxyz’
>>> y = r”xyz\nabc”
>>> x
’abc\\nxyz’
>>> print(x)
abc\nxyz
>>> y
’xyz\\nabc’
>>> print(y)
xyz\nabc
```
Keep in mind that the raw string notation does not create a different kind of string
either; rather it is a way of entering the string differently.
We have already seen functions and operators that apply to strings:

```
>>> x = ’77’
>>> len(x)
2
>>> int(x)
77
```
We’ve also seen that there are methods that apply specifically to strings. Recall that
there is a different syntax for methods. For example:
```
>>> x = ’a Hat’
>>> x
’a Hat’
>>> x.count(’a’)
2
>>> x.upper()
’A HAT’
>>> x.lower()
’a hat’
```
An extremely useful method for strings is `format()`. The basic idea is that you
define a string with empty slots and then fill those slots later with the `format()`
method. Slots are indicated with `{}`. So we can define a suitable string with one
slot like this:
```
>>> x = ’{} Mike’
We can then fill that slot any number of ways:
>>> y = x.format(’Hello’)
>>> y
’Hello Mike’
>>> z = x.format(’Goodbye’)
>>> z
’Goodbye Mike’
```
A string can have multiple slots. To fill them, the `format()` method can take
multiple arguments.
```
>>> x = ’{} Mike. {}?’
>>> x.format(’Hello’,’How are you’)
’Hello Mike. How are you?’
>>> x.format(’Privet’,’Kak dela’)
’Privet Mike. Kak dela?’
```
When a string does have multiple slots, then can be numbered (from 0). They are
then filled in that order by the arguments to `format()`.
```
>>> x = ’one = {1}; two = {0}’
>>> x.format(’dva’,’odin’)
’one = odin; two = dva’
```
In fact, the slots can be named and specified in the call to `format()`.
```
>>> x = ’one = {odin}; two = {dva}’
>>> x.format(dva=’dos’,odin=’uno’)
’one = uno; two = dos’
```
Finally, one can do simple spacing and alignment with the `format()` method.
You indicate the number of spaces to reserve for the argument with a preceding
colon. If the argument supplied by `format()` is less than the space reserved, you
indicate alignment to the left, right, or center with `<`, `>`, and `^` respectively.
```
>>> x = ’-{:<10}-’
>>> x.format(’hat’)
’-hat -’
>>> x = ’-{:>10}-’
>>> x.format(’hat’)
’- hat-’
>>> x = ’-{:^10}-’
>>> x.format(’hat’)
’- hat -’
```
Notice how when there is an odd number of remaining spaces, the extra goes to
the right.

Finally, there is a syntax for extracting part of a string. The syntax is to put one
or more integers in square brackets after the string. Using a single integer in the
square brackets extracts a single character. The characters in a string are counted
from the left, starting at 0.
For example:
```
>>> x = ’happiness’
>>> x[1]
’a’
>>> x[5]
’n’
```
One can also refer to a sequence of characters by using two integers separated by
a colon. The first index is the starting point of the sequence; the second index is
just after the end of the sequence. Thus something like `[2:4]` starts at the item
with index `2` and extends to just before the item with index `4`, thus the item with
index `3`. Since indexing starts at `0`, this span goes from the third character in the
string to the fourth character.
```
>>> x = ’abcde’
>>> x[2:4]
’cd’
```
Thus `x[n:n+1]` is the same as `x[n]`. If we have `x[n:m]` where `m < n+1`, we
end up with an empty string. For example:
```
>>> x = ’abcde’
>>> x[2:2]
’’
>>> x[2:1]
’’
```
Interestingly, we can leave out either integer when the colon is present. Leaving out
the first returns the entire string up to just before the integer that’s present. Leaving
out the second, gives the entire string starting from the first integer present. For
example:
```
>>> x = ’abcde’
>>> x[2:]
’cde’
>>> x[:2]
’ab’
```

4. **Lists**

Lists are an extremely important datatype: a single structure that holds a sequence
of elements of whatever type you want. You can create a list by simply listing
elements in square brackets. For example:
```
>>> x = [1,6,4,9]
>>> y = [’stops’,’fricatives’,’glides’]
>>> z = [7,’hats’,56,’chairs’,6.802]
```
The `len()` command also applies to lists:
```
>>> len(x)
4
>>> len(y)
3
>>> len(z)
5
```
You can also index into a list, as with a string:
```
>>> x[1]
6
>>> y[0]
’stops’
>>> z[3:]
[’chairs’,6.802]
```
There are lots of methods for dealing with lists. For example, the `append()`
method adds an element at the end of the list:
```
>>> x = [’rocks’,’paper’]
>>> x
[’rocks’,’paper’]
>>> x.append(’scissors’)
>>> x
[’rocks’, ’paper’, ’scissors’]
```
The `pop()` method is quite interesting. It removes an element at a specified index
position in a list. The method returns that element, altering the list at the same
time.
```
>>> x = [’stops’,’fricatives’,’glides’]
>>> x.pop(1)
’fricatives’
>>> x
[’stops’,’glides’]
```
The mirror-image method is `insert()`, which takes two arguments, the index
and the element to insert. The element is inserted just before the index you specify.
```
>>> x = [’stops’,’fricatives’,’glides’]
>>> x.insert(1,’hello!’)
>>> x
[’stops’,’hello!’,’fricatives’,’glides’]
```
A function that will turn out to be quite useful later on is `range()`. This takes a
single integer argument and returns a range object that represents the sequence
from 0 up to that argument. This can be directly converted to a list with the
`list()` function. For example:
```
>>> x = list(range(4))
>>> x
[0,1,2,3]
```
We also have the `sort()` and `reverse()` methods. The first sorts a list and
the second reverses it. Note that `sort()` only works for a list of uniform objects
that are sortable.
```
>>> x = [5,2,8,3]
>>> x.sort()
>>> x
[2,3,5,8]
>>> x = [5,2,8,3]
>>> x.reverse()
>>> x
[3,8,2,5]
```
Finally, we have the in operator which we can use to test for membership in a list:
```
>>> x = [5,2,8,3]
>>> 8 in x
True
>>> 7 in x
False
```

5. **Tuples**

Another datatype that you will see quite often is a tuple, a fixed sequence of elements,
similar to lists in many ways. The key difference is that tuples are fixed in
length and, once created, cannot be changed.
You create a tuple with parentheses. An empty tuple is just parentheses: `()`. Larger
tuples separate the members with commas, e.g. `(7,’hat’,8.2)`. Interestingly,
a tuple with one element must have a comma, unlike a list with a single
element: `(3,)`.
```
>>> x = ()
>>> y = (7,’hat’,8.2)
>>> z = (3,)
The len() function applies to tuples and you can index tuples just like lists.
>>> y = (7,’hat’,8.2)
>>> len(y)
3
>>> y[2]
8.2
```
The `in` operator applies to tuples, just as it does to lists:
```
>>> x = (5,2,8,3)
>>> 8 in x
True
>>> 7 in x
False
```
Finally, we can convert a list to a tuple with `tuple()` or a tuple to a list with
`list()`:

```
>>> x = [1,2,3]
>>> type(x)
<class ’list’>
>>> y = tuple(x)
>>> type(y)
<class ’tuple’>
>>> a = (1,2,3)
>>> type(a)
<class ’tuple’>
>>> b = list(a)
>>> type(b)
<class ’list’>
```

6. **Dictionaries**

One of the most useful datatypes for linguists are dictionaries. Dictionaries are effectively
sets of pairs, where the first element in the pair can be used to “look up” the
second. The set of first elements must thus be unique. A dictionary is marked with
curly brackets where each pair of elements is separated with a colon. For example:
```
>>> d = {’cat’:7,’chair’:’hat’,’table’:7}
```
Notice how ’cat’, ’chair’, and ’table’ are distinct, but 7, ’hat’, and 7
do not need to be. We refer to the first member of each pair as a key and the second
as its value. We look up values by putting the key in square brackets after the name
of the dictionary:
```
>>> d = {’cat’:7,’chair’:’hat’,’table’:7}
>>> d[’cat’]
7
>>> d[’chair’]
’hat’
```
The `len()` function can apply to a dictionary and returns the number of pairs in
the dictionary:
```
>>> d = {’cat’:7,’chair’:’hat’,’table’:7}
>>> len(d)
3
```
We can add new pairs to a dictionary simply by assigning to a new key:
```
>>> d = {’cat’:7,’chair’:’hat’,’table’:7}
>>> d[’onion’] = 3.7
>>> len(d)
4
```
We can test for whether any specific item is a key in a dictionary with in. For
example:
```
>>> d = {’cat’:7,’chair’:’hat’,’table’:7}
>>> ’chair’ in d
True
>>> ’hat’ in d
False
```
Notice how in tests for membership in the dictionary keys, not the dictionary
values.
Dictionary items can be altered or deleted.
```
>>> d = {’cat’:7,’chair’:’hat’,’table’:7}
>>> d[’cat’] = d[’cat’] + 2
>>> d[’cat’]
9
>>> del(d[’cat’])
>>> d
{’chair’:’hat’,’table’:7}
```
We can extract the keys, values, or key–value pairs from a dictionary. These are
returned as specific datatypes, but all can be converted to lists with `list()`. For
example:
```
>>> d = {’cat’:7,’chair’:’hat’,’table’:7}
>>> list(d.keys())
[’chair’, ’cat’, ’table’]
>>> list(d.values())
[’hat’, 7, 7]
>>> list(d.items())
[(’chair’, ’hat’), (’cat’, 7), (’table’, 7)]
```
Finally, dictionaries can be used directly with the `format()` method for strings.
There’s a special operator for this `**`. The basic idea is that the slots in the string
are named. The values that go in those slots are associated with the relevant keys
of the dictionary. For example:
```
>>> d = {’uno’:’eins’,’dos’:’zwei’,’tres’:’drei’}
>>> s = ’one = {uno} and three = {tres}’
>>> s.format(**d)
’one = eins and three = drei’
```
Notice that keys of the dictionary that are not named in the string are simply disregarded.

## Mutability

Mutability can only be detected when an element has multiple parts. The idea would be that you could change
some part of an element and leave the rest intact. This is possible for lists and
dictionaries; they are mutable. Thus, we can define a list and then add or delete
elements in that list, or change elements in the list. For example:
```
>>> x = [’Tom’,’Dick’,’Harry’]
>>> x[1] = ’Mary’
>>> x
[’Tom’,’Mary’,’Harry’]
>>> x.append(’Edna’)
>>> x
[’Tom’,’Mary’,’Harry’,’Edna’]
```
We’ve already seen the `insert()` and `pop()` methods, which both allow us to change a list.
Dictionaries are also mutable. We can add, delete, or change items. For example:
```
>>> d = {’un’:’un’,’deux’:’?’,’trois’:’tri’}
>>> d[’quatre’] = ’pedwar’
>>> d[’deux’] = ’dau’
>>> d
{’un’:’un’,’deux’:’dau’,’trois’:’tri’,
’quatre’:’pedwar’}
```
As noted above, for simple datatypes like numbers and booleans, we cannot see the
effects of their immutability. Superficially, it seems like we can change them:
```
>>> x = 3
>>> x = 7
>>> x
7
>>> y = True
>>> y = False
>>> y
False
```
This is only apparent however. In both cases above, we are simply reassigning
the names `x` and `y` to new elements. The old elements are unchanged, though
available for garbage collection.
Strings and tuples have multiple parts, but are not mutable. For example, while we
can refer to pieces of each with indexes, we cannot assign new values to just those
indexed segments. For strings:
```
>>> x = ’abc’
>>> x[1] = ’d’
Traceback (most recent call last):
File ”<stdin>”, line 1, in <module>
TypeError: ’str’ object does not
support item assignment
```
The same applies to tuples:
```
>>> x = (’a’,’b’,’c’)
>>> x[1] = ’d’
Traceback (most recent call last):
File ”<stdin>”, line 1, in <module>
TypeError: ’tuple’ object does not
support item assignment
```
Notice that we can reuse a name that was assigned initially to a string or tuple, but
this is reusing the name, not changing the initial data structure.
```
>>> x = ’a first string’
>>> x = ’another string’
```
Note that methods for mutable and immutable elements differ in whether
they change the object they are methods for or return a new element. On the
one hand, the `reverse()` method for lists alters the list in place, reversing its
elements. On the other hand, the `upper()` method for strings returns a new
string with all uppercase letters and leaves the initial string unaffected.
```
>>> x = [1,2,3]
>>> x.reverse()
>>> x
[3,2,1]
>>> y = ’letters’
>>> y.upper()
’LETTERS’
>>> y
’letters’
```
