
## Control Structures

This handout is about how statements can be executed conditionally, how some
statements can escape being executed and how others can be executed any number
of times.

#### Grouping and indentation

To make full use of control structures, we need to understand how Python groups
statements together. To understand this, let's look at the `if` control structure. This
structure, in it's simplest form, allows for conditional application. There is a test
clause and then a block of one or more statements. If the test clause is true, the
statements are executed. If it is not true, the statements are not executed. Here's
an example:


```python
#a single statement can occur
#on the same line
if 2 + 2 == 4: print('that was true')
```

    that was true
    


```python
#a single statement can occur
#indented on the next line
if 2 + 2 == 4:
    print('that was true')
```

    that was true
    

The test is introduced with the keyword `if` and terminates with a colon. If the
statement block is a single statement, it can occur on the same line or the next. If
it occurs on the next line, it must be spaced or tabbed (four spaces or a tab).
If there is no indentation, an error is produced. The example below demonstrates.
Note that we have added a comment to the code to remind us that this file does
not work. Comments are indicated with a `#` on the left side of the line and have no
effect on the code. If you run this or any other program, comments have no effect.


```python
#produces an error
if 2 + 2 == 4:
print('that was true')
```


      File "<ipython-input-5-95df98541a1f>", line 3
        print('that was true')
            ^
    IndentationError: expected an indented block
    


If there are multiple statements contingent on the test, then they must appear on
separate lines and they must be tabbed or spaced in the same amount. Here's a wellformed
example:


```python
#multiple statements correctly indented
if 2 + 2 == 4:
    print('that was true')
    print('...really true')
```

    that was true
    ...really true
    

Here's an ill-formed example; the second statement has an extra space.


```python
#produces an error
if 2 + 2 == 4:
    print('that was true')
      print('...really true')
```


      File "<ipython-input-7-ccddd92e72ab>", line 4
        print('...really true')
        ^
    IndentationError: unexpected indent
    


A similar error occurs if the first of the two statements has an extra indentation:


```python
#produces an error
if 2 + 2 == 4:
      print('that was true')
    print('...really true')
```


      File "<ipython-input-8-91ec9d0bc812>", line 4
        print('...really true')
                               ^
    IndentationError: unindent does not match any outer indentation level
    


In principle, you can indent with either spaces or tabs (https://stackoverflow.blog/2017/06/15/developers-use-spaces-make-money-use-tabs/), but be careful and do not mix
them! For example, if you indent one line with a tab and then indent the next line
with the right number of spaces so that they look aligned, this will typically generate
an error. The problem is that Python has no way of knowing how wide you’ve set
your tabs to display in your word processor.

Note that this tabbing has semantic consequences. Compare the following:


```python
#block has two statements in it
if 2 + 2 == 5:
    print("that shouldn't happen")
    print('or this....')
```


```python
#block has one statement in it
if 2 + 2 == 5:
    print("that shouldn't happen")
print('or this....')
```

    or this....
    

In both cases, we test `if 2 + 2 == 5`; that evaluates to false. In the first example,
the two statements are not executed since they are in the block of contingent
statements. In the second case, the second statement is executed. Since it is not
indented, it is evaluated as outside of the `if` structure and thus not contingent on
the `if` test.

This semantic effect also shows itself with nested if structures. In the following
example, we first test `if 2 + 2 == 4`. If that is true, which of course it is, then we
execute the following three statements. We first print `'wow'`. Second, we execute
another if structure. This second if structure tests `if 7 * 7 == 48`, which is false. If
it were true, we would print `'wow again'`. Finally, the third statement in the
initial if structure's block prints `'wow a third time'`.


```python
#nested if with following statement
if 2 + 2 == 4:
    print('wow')
    if 7 * 7 == 48:
        print('wow again')
    print('wow a third time')
```

    wow
    wow a third time
    

In the next example, we've spaced/tabbed in the final statement so that it is part
of the nested if structure. It will only execute if both if tests evaluate to true.


```python
if 2 + 2 == 4:
    print('wow')
    if 7 * 7 == 48:
        print('wow again')
        print('wow a third time')
```

    wow
    

Finally, in this third case, the final statement has no indentation. It therefore is
executed regardless of the two tests.


```python
if 2 + 2 == 4:
    print('wow')
    if 7 * 7 == 48:
        print('wow again')
print('wow a third time')
```

    wow
    wow a third time
    

Let’s now look a little more closely at the options for `if`. We’ve already seen that
one or more statements can be contingent on some logical test. If the test evaluates
to `true`, the block of statements then executes in order. If it is `false`, none of them is
executed.

A very simple augmentation of the if structure is the `else` clause. This is a block
of code that executes if the `if` test evaluates to `false`. The `else` statement follows
the first block of code and is at the same level of indentation as the initial `if` clause.
For example:


```python
#only else block executes
if 2 + 2 == 5:
    print("this won't print")
else:
    print('but this will')
    print('...and so will this')
```

    but this will
    ...and so will this
    

If the `if` clause evaluates to `true`, the `else` block will not execute:


```python
#else-block does not execute
if 2 + 2 == 4:
    print("this won't print")
else:
    print('but this will')
    print('...and so will this')
```

    this won't print
    

Finally, one can add any number of `elif` clauses to an `if` structure. These add
additional contingent tests to the structure. The syntax is like this:
```
if test1
    block1
elif test2
    block2
elif test3
    block3
...
else
    blockn
```

Notice how if `test1` is true, `block1` applies regardless of the truth or falsity of
any other test. If `test1` is false and `test2` is true, `block2` applies regardless
of whether `test3` is true. Finally, the `else` block only applies if all previous tests
are false.

A final complication is that it may sometimes be convenient to have an empty block.
Imagine you want to test a string for whether the first letter is `'a'`, but then do
something in all other cases. One way to do this is to test for that, but then put
your code in the else block. The problem with this is that you would then have
an empty block following the `if` test. This is not allowed in Python. To deal with
this possibility, Python has the pass statement which you can use to fill the block.
For example:


```python
#set a variable
x = 'hat'
#if clause with empty block
if x[0] == 'a':
    pass
else:
    print('doing something here....')
```

    doing something here....
    

Here the print statement only happens when the first letter of the string is not
'a'.

#### Digression about the `print` command

We’ve already seen that it can be given a string as an argument and prints that
string:


```python
print('here is a string')
```

    here is a string
    

It can also be given any number of strings; they are all printed to the screen:


```python
print('one','two','three')
```

    one two three
    

Notice that the strings are separated by spaces. We can specify another separator or,
indeed, no separator with the optional `sep` argument. If we include this argument,
we specify its value with `=`. For example:


```python
print('one','two','three',sep = '-')
print('one','two','three',sep = '')
```

    one-two-three
    onetwothree
    

Finally, notice that the default behavior for `print()` is to print its argument(s)
and begin a new line. We can specify different behavior by giving a value to the
optional end argument.


```python
print('one','two',sep = '-', end = '!')
print('not on the next line')
```

    one-two!not on the next line
    

#### `for`

The `for` control structure allows for multiple application of some fixed block of
code. You specify a list or sequence of items and then iterate over the list applying
the block once for each item in the list or sequence. The syntax is a `for` clause
followed by an indented block of one or more statements. The `for` clause begins
with the keyword `for`, then a variable name, then the `in` operator, then a list or
sequence of items that can be iterated over, and finally a colon.


```python
for i in [1,2,3]:
    print(i)
```

    1
    2
    3
    

Here we assign the variable `i` the values from the list `[1,2,3]` one by one. For
each assignment, we apply the block. In this case, the block simply prints the value
of `i`. What do we have to change to print the result on one line?

Note that nothing requires that we actually use the value `i` in the block. Thus the
following works as well:


```python
#value for i not used
for i in [1,2,3]:
    print('wow')
```

    wow
    wow
    wow
    

Similarly, nothing prevents us from using the variable more than once per each
iteration. For example:


```python
#using the variable twice
for i in [1,2,3]:
    print('{} + 2 = {}'.format(i,i+2))
```

    1 + 2 = 3
    2 + 2 = 4
    3 + 2 = 5
    

We can iterate over strings as well. For example:


```python
#printing letters separated by spaces
for i in 'tone':
    print(i,end=' ')
#add a return at the end
print()
```

    t o n e 
    

Here we print each letter separately. We end each print operation with a space
rather than a return. Then, after all that printing, we get back to the beginning of
the line by printing nothing. Since the default is to end each printed item with a
return, printing nothing has the effect of starting a new line.

Recall the `range()` function. We can iterate directly
over the sequence of numbers it provides. For example, if we want to add up all
the numbers from 0 to 4, we can do it like this:


```python
#set a variable
total = 0
#iterate and add to total
for i in range(5):
    total = total + i
#print the total
print(total)
```

    10
    

Here we first define a variable `total` and set its value to 0. We then create a
sequence from 0 to 4 (the integer value just before the value specified). Then on
each iteration we reset the value of `total` to be equal to its current value plus the
current value of `i`.

This is a fairly common programming technique, create a variable that we incrememtally
change in some sort of loop. We can do some fairly interesting stuff with
this. For example, we might do morphological recursion with this:


```python
#initial prefix and word
prefix = 'anti'
word = 'missle'
#print the word
print(word)
#iterate 3 times
for i in range(3):
    #add a prefix to the word...
    word = prefix + '-' + word
    #...and print the new word
    print(word)
```

    missle
    anti-missle
    anti-anti-missle
    anti-anti-anti-missle
    

There are a couple of things that distinguish this from the previous example. First,
notice that we are doing string concatenation, rather than addition. Second, notice
that we are printing the word variable at each iteration, rather than just at the end.
This then is an instance of the semantic effects of indentation in a real example. If
we had not indented the final `print` statement, this would have simply printed the
last line above.

As with `if`, we can nest `for` structures. Thus, we can augment our prefixation
example above, so that it prefixes multiple words:


```python
#define the prefix and 3 words
prefix = 'anti'
words = ['missle','racism','music']
#iterate over each word
for word in words:
    #print the word
    print(word)
    #for each word, iterate 3 times
    for i in range(3):
        #add the prefix to the current word
        word = prefix + '-' + word
        #print the new word
        print(word)
```

    missle
    anti-missle
    anti-anti-missle
    anti-anti-anti-missle
    racism
    anti-racism
    anti-anti-racism
    anti-anti-anti-racism
    music
    anti-music
    anti-anti-music
    anti-anti-anti-music
    

The other thing to notice here is that for allows us to do potentially massive calculations
with finite means. For example, if we wanted to sum numbers up to 10,000,
this would be a trivial change to the code above.


```python
#variable to accumulate additions
total = 0
#iterate a lot
for i in range(10000):
    #add i to total
    total = total + i
#print the total
print(total)
```

    49995000
    

Now that we have two control structures, `if` and `for`, we can combine them.
Let’s write some code to count the vowels in a string.


```python
#define vowels
vowels = 'aeiou'
#variable to accumulate the vowel count
vowelCount = 0
#define the word
word = 'Appalachicola'
#go through the word letter by letter
for letter in word:
    #for each letter check if it’s a vowel
    if letter in vowels:
        #if it is, add 1 to the total
        vowelCount = vowelCount + 1
#print the total
print(vowelCount)
```

    5
    

Here we first define vowels. We then set our count of vowels to 0. We define the
word we will count vowels in. Next we iterate through each letter in the word
assigning the current letter to the variable letter. We then test if that letter is
a vowel with the `in` operator. If it is, we augment the value of `vowelCount` by
one. If is not a vowel, that test fails, nothing happens and we go on to the next
iteration. Finally, we print the value of `vowelCount`.

The operation where we augment a variable by some specific amount is frequent
enough that there is a special operator for it: `+=`. The following does exactly the
same thing as the preceding.


```python
#define vowels
vowels = 'aeiou'
#variable to accumulate the vowel count
vowelCount = 0
#define the word
word = 'Appalachicola'
#go through the word letter by letter
for letter in word:
    #for each letter check if it’s a vowel
    if letter in vowels:
        #if it is, add 1 to the total
        vowelCount += 1
#print the total
print(vowelCount)
```

    5
    

We can also nest a `for` loop inside of an `if` structure. Here we set up virtually the
same initial variables. We then test if the first letter of the word is a vowel. Note
that since we’ve defined vowels as lowercase letters, we must first convert the first
letter to lowercase. If the word does begin with a vowel, we count all the letters.
(Of course, we could have simply used the `len()` function!)


```python
#define vowels
vowels = 'aeiou'
#set counter to zero
letterCount = 0
#define the word
word = 'Appalachicola'
#convert first vowel to lowercase
#is it a vowel?
if word[0].lower() in vowels:
    #if it is go through letter by letter
    for letter in word:
        #for each letter, add 1
        letterCount += 1
#do this if the word is not V-initial
else:
    print('Not vowel-initial')
#print the number of letters
print(letterCount)
```

    13
    

Make sure you understand the semantics of control structures like `if` and `for`
and what it means for them to be nested in different ways. Writing programs is mostly
about figuring out the logic of the problem you want to solve and then recasting it in terms of nested
control structures.

#### `while`

Technically, the `for` control structure isn’t necessary. Anything you can do with
`for`, you can do with `while`, perhaps a bit awkwardly. The logic of `while`
is that a statement or block of statements is iterated as long as some test holds
true.

The syntax is parallel to what we have seen already. There is the keyword
`while`, followed by the test, an expression that returns a boolean value, followed
by a colon. There is then an indented block of one or more statements. If there is
only one statement, it can appear on the same line as the `while` test. Here it is
schematically:

```
while x == y:
    dosomething(z)
    dosomethingelse(w)
```

Here we have a test for equality between some variables `x` and `y`. We then have a
block of two statements. We first check the test. If it is true, we apply the statements
in the block. We then go back and check the test again. If it is still true, we apply
the statements again. We go through this loop until the test returns `False`.

This should seem a bit silly. If the test returns `True` then it should always return
`True` and we should loop forever. That’s not typically what we want! The way this
structure is typically used is that the truth value of the test is changed during the
block of statements so that it eventually becomes false. Here’s a simple example:


```python
#set counter
count = 0
#check value of counter
while count < 3:
    #increment counter
    #escape clause!
    count += 1
    print(count)
```

    1
    2
    3
    

First we define a variable `count` and store the number 0 in it. We then begin our
`while` structure by testing whether `count` is less than 3, which of course it is. If
we did not alter the value of count in the block of statements, this would iterate
forever. What we do though is to increment the value of count at each iteration.
It will eventually reach 3, the test will then fail, and the iteration will cease.

It’s important to keep track of what happens when. Very small changes can change
the outcome; for example, imagine we reverse lines 3 and 4 like this:


```python
#declare counter
count = 0
#check value of counter
while count < 3:
    #print the value
    print(count)
    #NOW increment the counter
    count += 1
```

    0
    1
    2
    

It’s also very easy to get this wrong and inadvertantly get an infinite loop. For
example:
```
#error: infinite loop!
while count < 3:
    count = 0
    print(count)
    count += 1
```
Here we’ve moved the initial assignment to `count` into the body of the `for` loop.
This means that in every loop, we reset the variable to 0 and then add 1; it will thus always be less than 3.

As with the other control structures we have seen, `while` can combine with itself
and with other structures. Here is an example of `while` nested within `while`:


```python
#define the word
word = 'alphabet'
#define the counter
count = 0
#iterate while the counter is
#less than the length of the word
while count < len(word):
    #print the current letter
    print(word[count])
    #increment the counter
    count += 1
    #start a new counter
    othercount = 1
    #check that the new counter is
    #less than the original one
    while othercount < count + 1:
        #print ever larger prefixes of the word
        print('\t',word[0:othercount])
        #increment the other counter
        othercount += 1
```

    a
    	 a
    l
    	 a
    	 al
    p
    	 a
    	 al
    	 alp
    h
    	 a
    	 al
    	 alp
    	 alph
    a
    	 a
    	 al
    	 alp
    	 alph
    	 alpha
    b
    	 a
    	 al
    	 alp
    	 alph
    	 alpha
    	 alphab
    e
    	 a
    	 al
    	 alp
    	 alph
    	 alpha
    	 alphab
    	 alphabe
    t
    	 a
    	 al
    	 alp
    	 alph
    	 alpha
    	 alphab
    	 alphabe
    	 alphabet
    

First we assign the string 'alphabet' to the variable word and the integer 0 to
the variable count. The outer `while` loop goes through the string letter by letter
and prints them out. It increments the count variable on each loop to keep track
of the iteration and to determine which letter to print. The inner `while` loop is a
little more complex. It prints out prefixes (initial substrings) of the word based on
the current letter determined by the outer while loop. Thus, for example, when
the current letter is 'h', the inner `while` loops prints out a, al, alp, and alph.
Notice how the test for the inner `while` loop refers to the variable count as well
as othercount, which change on the outer and inner loops respectively.

The `while` structure can, of course, combine with other control structures. For
example, here is a case of `if` inside `while`:


```python
#set the word
word = 'alphabet'
#define vowels
vowels = 'aeiou'
#set the counter
count = 0
#iterate
while count < len(word):
    #get the current letter
    letter = word[count]
    #is it a non-vowel
    if letter not in vowels:
        #if so, print it
        print(letter)
    #increment counter
    count += 1
```

    l
    p
    h
    b
    t
    

The `while` structure is very similar to the `for` structure and it’s always possible to
translate back and forth. For example, recall the first example of the `for` structure, repeated below:

```
for i in [1,2,3]:
    print(i)
```
We can translate this into a `while` structure like this:
```
i = 1
while i < 4:
    print(i)
    i += 1
```
The upshot is that the choice between these typically depends on the which makes
the code more intelligible to you as the programmer.

Finally, the `while` structure also allows for a block of `else` statements.
These are executed when the `while` test is or becomes false. The general
syntax is as follows:
```
while ...:
    statement(s)
else:
    statement(s)
```


```python
#define vowels
vowels = 'aeiou'
#set the word
word = 'Winnepesaukee'
#create two counters
counter = 0
vowelcount = 0
#go through letter by letter
while counter < len(word):
    #is current letter a vowel?
    if word[counter] in vowels:
        vowelcount += 1
    #keep track of total number of letters
    counter += 1
#when counter is too big, do this:
else:
    print('There are',vowelcount,'vowels in this word')
```

    There are 7 vowels in this word
    

#### `break` and `continue`

We can impose finer control on `for` and `while` with the `break` and `continue`
statements. The `break` statement exits from the smallest enclosing `for` or `while`
loop. The `continue` statement exits from the current iteration of the smallest
enclosing `for` or `while` loop and moves to the next iteration. Here’s an example of `break`:


```python
#define vowels and word
vowels = 'aeiou'
word = 'sthenic'
#set up a counter
counter = 0
#iterate through the word letter by letter
while counter < len(word):
    #if the current letter is a vowel,
    #exit the loop
    if word[counter] in vowels:
        break
    #don’t forget to update the counter!
    counter += 1
#print value of counter when break occurred
print('The word begins with',counter,'consonant letters')
```

    The word begins with 3 consonant letters
    

Here we define a specific word and vowel letters. We then check whether each
letter is a vowel. If it is, we break/exit from the `while` loop. We then print the
value of counter, which is the number of letters iterated through to get to the
`break` statement.

Note that it’s fairly easy to make errors in getting the right count here. We start
with counter set to 0, which allows us to use it to access each letter of the word,
remembering that the indices of the word begin with 0.

We increment counter after the `if` structure. When the `if` structure test is true,
the value of counter is the index of the first vowel letter, the index just past the
last consonant letter. Since indices start at 0, this means that the value of counter
when we exit is also the total number of consonants in the initial span.

The break statement also works with a `for` loop. For example, here is the equivalent
to the previous example, replacing `while` with `for`:


```python
#define vowels and word
vowels = 'aeiou'
word = 'sthenic'
#initialize counter
counter = 0
#go through all letters
for i in range(len(word)):
    #is current letter a vowel?
    if word[i] in vowels:
        #if so, exit the loop
        break
    #don’t forget to update the counter
    counter += 1
#print result
print('The word begins with',
counter,'consonant letters')
```

    The word begins with 3 consonant letters
    

With the `break` statement available to us to exit the `while` loop, we can use
`while` tests that are always true, relying on the `break` statement to exit the loop
when we want. For example:


```python
#define vowels and the word
vowels = 'aeiou'
word = 'sthenic'
#initialize the counter
counter = 0
#iterate forever
while True:
    #is current letter a vowel?
    if word[counter] in vowels:
        #if so, exit
        break
    #remember to increment counter
    counter += 1
#print result
print('The word begins with',
counter,'consonant letters')
```

    The word begins with 3 consonant letters
    

Note that the `while` test will always be true so the loop will continue forever unless
the `if` test becomes true at some point so that `break` can be executed, exiting the
`while` loop. Thus it’s important that you be very sure `break` is contingent on a
test that will be true at some point if the enclosing loop is always true.

Slightly different behavior is obtained with the `continue` statement. As with
`break`, it is used inside a `for` or `while` loop. What it does is exit the current
iteration and goes on to the next iteration. Schematically, we have something like
this:
```
for ...:
    some statements
    if ...:
        continue
    more statements
```

We have some iterative structure like `for`. We then have zero or more statements.
Somewhere in the body we have a `continue` statement, typically in the body
of some `if` structure. Following the `if`/`continue`, we have some number of
additional statements. What happens is that the `for` licenses some number of
iterations. At each iteration, the initial statements apply, then the `if` test occurs.
If the `if` test is false, the `continue` statement is not executed and the additional
following statements get to apply.

If the `if` test is true on some iteration, then the `continue` statement does apply
and the statements following `if`/`continue` do not apply on that iteration. We
continue with the next iteration, however, unlike with `break` where all iteration
ends. Here’s a simple example:


```python
#define vowels and the word
vowels = 'aeiou'
word = 'sthenic'
#initialize counter
counter = 0
#go through each letter
for i in range(len(word)):
    #is the current letter a vowel?
    if word[i] in vowels:
        #if so, skip it
        continue
    #increment counter (only for non-vowels!)
    counter += 1
#print result
print('The word has',
counter,'consonant letters')
```

    The word has 5 consonant letters
    

Here we set up some initial variables. We then enter a `for` loop based on the length
of the string variable word. At each iteration, we test whether the current letter in
the string is a vowel. If it is not a vowel, we increment the `counter` variable. If it
is a vowel, we go to the next iteration, not incrementing the `counter` variable. In
other words, the `counter` variable is incremented only when the current letter is
not a vowel. Once we exit the iteration, we print the value of `counter`.

You can also use a `continue` statement inside of a `while` structure. The following
relatively inefficient code snippet exemplifies this and has the same result
as the preceding one.


```python
#set up initial variables
vowels = 'aeiou'
word = 'Mississippi'
counter = 0
i = 0
#go through word letter by letter
while i < len(word):
    #is the current letter a vowel?
    if word[i] in vowels:
        #if so, increment letter count
        i += 1
        #...and exit current loop
        continue
    #otherwise, increment letter count
    i += 1
    #increment consonant count
    counter += 1
#print result
print('The word has',
counter,'consonant letters')
```

    The word has 7 consonant letters
    

#### Making nonsense items

Let’s use the control structures we’ve learned here to build a program that does
something useful. A frequent task for psycholinguists is finding items for experiments,
either items that directly exemplify some property we want to test or items
that fill out an experiment and can be used to distract subjects from the true goal
of the experiment.

Imagine what we want are CV monosyllables. We could just try to think of all
possible monosyllables with a CV shape, but another way to go is to generate these
programmatically. If we know what the possible consonants are and what the possible
vowels are, we can generate a list of possible CV monosyllables quite simply.
Here’s a first pass:


```python
#define vowels and consonants
vowels = 'aiu'
consonants = 'ptk'
#for every vowel
for v in vowels:
    #choose a consonant
    for c in consonants:
        #now print them together
        print(c,v,sep='')
```

    pa
    ta
    ka
    pi
    ti
    ki
    pu
    tu
    ku
    

This program defines a set of consonants and a set of vowels and then prints out all
possible combinations. As such, it’s a bit silly. In the case at hand, there are only
nine possible combinations and we could just as easily listed those out. This approach
becomes more reasonable though if the number of consonants and vowels
increases:


```python
#define vowels and consonants
vowels = 'aeiou'
consonants = 'ptkbdg'
#for every vowel
for v in vowels:
    #choose a consonant
    for c in consonants:
        #now print them together
        print(c,v,sep='')
```

    pa
    ta
    ka
    ba
    da
    ga
    pe
    te
    ke
    be
    de
    ge
    pi
    ti
    ki
    bi
    di
    gi
    po
    to
    ko
    bo
    do
    go
    pu
    tu
    ku
    bu
    du
    gu
    

We might also want CVC syllables among our items. This is easy to do as well:


```python
#define Vs and Cs
vowels = 'aeiou'
consonants = 'ptkbdg'
#for every vowel:
for v in vowels:
    #choose a consonant
    for o in consonants:
        #now choose another consonant
        for c in consonants:
            #print them together
            print(o,v,c,sep='')
```

    pap
    pat
    pak
    pab
    pad
    pag
    tap
    tat
    tak
    tab
    tad
    tag
    kap
    kat
    kak
    kab
    kad
    kag
    bap
    bat
    bak
    bab
    bad
    bag
    dap
    dat
    dak
    dab
    dad
    dag
    gap
    gat
    gak
    gab
    gad
    gag
    pep
    pet
    pek
    peb
    ped
    peg
    tep
    tet
    tek
    teb
    ted
    teg
    kep
    ket
    kek
    keb
    ked
    keg
    bep
    bet
    bek
    beb
    bed
    beg
    dep
    det
    dek
    deb
    ded
    deg
    gep
    get
    gek
    geb
    ged
    geg
    pip
    pit
    pik
    pib
    pid
    pig
    tip
    tit
    tik
    tib
    tid
    tig
    kip
    kit
    kik
    kib
    kid
    kig
    bip
    bit
    bik
    bib
    bid
    big
    dip
    dit
    dik
    dib
    did
    dig
    gip
    git
    gik
    gib
    gid
    gig
    pop
    pot
    pok
    pob
    pod
    pog
    top
    tot
    tok
    tob
    tod
    tog
    kop
    kot
    kok
    kob
    kod
    kog
    bop
    bot
    bok
    bob
    bod
    bog
    dop
    dot
    dok
    dob
    dod
    dog
    gop
    got
    gok
    gob
    god
    gog
    pup
    put
    puk
    pub
    pud
    pug
    tup
    tut
    tuk
    tub
    tud
    tug
    kup
    kut
    kuk
    kub
    kud
    kug
    bup
    but
    buk
    bub
    bud
    bug
    dup
    dut
    duk
    dub
    dud
    dug
    gup
    gut
    guk
    gub
    gud
    gug
    

The same kind of logic can be used to construct sentences. Imagine we want every possible SVO sentence in some (nonsense) language. We have a set of nouns and transitive verbs. We can combine them straightforwardly:


```python
#every possible N and V
nouns = 'cat flower monkey'
verbs = 'ate kissed watered saw'
#every possible SVO combo
for s in nouns.split():
    for v in verbs.split():
        for o in nouns.split():
            #print combination
            print(s,v,o)
```

    cat ate cat
    cat ate flower
    cat ate monkey
    cat kissed cat
    cat kissed flower
    cat kissed monkey
    cat watered cat
    cat watered flower
    cat watered monkey
    cat saw cat
    cat saw flower
    cat saw monkey
    flower ate cat
    flower ate flower
    flower ate monkey
    flower kissed cat
    flower kissed flower
    flower kissed monkey
    flower watered cat
    flower watered flower
    flower watered monkey
    flower saw cat
    flower saw flower
    flower saw monkey
    monkey ate cat
    monkey ate flower
    monkey ate monkey
    monkey kissed cat
    monkey kissed flower
    monkey kissed monkey
    monkey watered cat
    monkey watered flower
    monkey watered monkey
    monkey saw cat
    monkey saw flower
    monkey saw monkey
    

As in the word-based example above, this is kind of silly when the sets of elements
we are combining are so small, but becomes more useful if we expand those sets.
What do we do if some of our verbs are intransitive? There are a number of ways
to deal with this; here’s a simple one:


```python
#Ns, Vs, & intransitives
nouns = 'cat flower monkey'.split()
verbs = 'ate kissed saw watered danced swam'.split()
ivs = 'danced swam'.split()
#for every N and V
for s in nouns:
    for v in verbs:
        #if the V is intransitive
        if v in ivs:
            print(s,v)
        #otherwise it’s transitive
        else:
            for o in nouns:
                print(s,v,o)
```

    cat ate cat
    cat ate flower
    cat ate monkey
    cat kissed cat
    cat kissed flower
    cat kissed monkey
    cat saw cat
    cat saw flower
    cat saw monkey
    cat watered cat
    cat watered flower
    cat watered monkey
    cat danced
    cat swam
    flower ate cat
    flower ate flower
    flower ate monkey
    flower kissed cat
    flower kissed flower
    flower kissed monkey
    flower saw cat
    flower saw flower
    flower saw monkey
    flower watered cat
    flower watered flower
    flower watered monkey
    flower danced
    flower swam
    monkey ate cat
    monkey ate flower
    monkey ate monkey
    monkey kissed cat
    monkey kissed flower
    monkey kissed monkey
    monkey saw cat
    monkey saw flower
    monkey saw monkey
    monkey watered cat
    monkey watered flower
    monkey watered monkey
    monkey danced
    monkey swam
    

Finally, imagine the language has a reflexive pronoun *vi* that replaces the object if
it is identical to the subject. We can incorporate this like this:


```python
#Ns, Vs, intransitives
nouns = 'cat flower monkey'.split()
verbs = 'ate kissed saw watered danced swam'.split()
ivs = 'danced swam'.split()
#for every S+V combo:
for s in nouns:
    for v in verbs:
        #if the verb is intransitive:
        if v in ivs:
            print(s,v)
        #otherwise (transitives)
        else:
            for o in nouns:
                #if subject and object are identical
                if s == o:
                    #replace O with reflexive
                    o = 'themselves'
                print(s,v,o)
```

    cat ate themselves
    cat ate flower
    cat ate monkey
    cat kissed themselves
    cat kissed flower
    cat kissed monkey
    cat saw themselves
    cat saw flower
    cat saw monkey
    cat watered themselves
    cat watered flower
    cat watered monkey
    cat danced
    cat swam
    flower ate cat
    flower ate themselves
    flower ate monkey
    flower kissed cat
    flower kissed themselves
    flower kissed monkey
    flower saw cat
    flower saw themselves
    flower saw monkey
    flower watered cat
    flower watered themselves
    flower watered monkey
    flower danced
    flower swam
    monkey ate cat
    monkey ate flower
    monkey ate themselves
    monkey kissed cat
    monkey kissed flower
    monkey kissed themselves
    monkey saw cat
    monkey saw flower
    monkey saw themselves
    monkey watered cat
    monkey watered flower
    monkey watered themselves
    monkey danced
    monkey swam
    
