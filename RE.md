
## Regular expressions

One of the most important aspects of programming for linguists is pattern matching. You will very often have to assess whether some string matches some pattern, contains some sequence of characters, some number of characters, etc.

We’ve already seen that we can do this with what we’ve already learned. For example, if we wanted to know if some string `s` contained the sequence `'ab'`, we could simply write `'ab'` in `s` which would return `True` or `False`. If, on the other hand, we wanted to know if a string contained `'a'` and then `'b'` with material potentially intervening, we would have to do more. We might write a function like this:


```python
s = 'hab'
'ab' in s
```




    True




```python
#a and then b
def mymatch(s):
  i = 0
  #a flag to keep track of
  #whether we see an ’a’
  aFlag = False
  while i < len(s):
    if s[i] == 'a':
      aFlag = True
      break
    i += 1
  #start looking for ’b’
  #where we left off
  while i < len(s):
    if s[i] == 'b':
      #if we find ’b’, return
      #True of False depending
      #on whether we previously
      #saw ’a’
      return aFlag
    i += 1
  #if all that fails, return False
  return False

print(mymatch('Alice in ab Barcelona'))
```

    True
    

We can test out how the function `mymatch()` applies to different strings. The logic of the function is that we search the string for the first instance of `'a'` by iterating across the string with the counter `i`. If we find it, we set the value of `aFlag` to `True` and exit the first `while` loop. Then, without resetting `i`, we initiate another `while` loop to look for `'b'`. Not resetting the value of `i` means that the second loop picks up where the first ended. Hence, the `'b'` must follow the (first) `'a'`.

This is fine as it goes, but it doesn’t generalize. There are an infinite number of patterns we might want to search for and writing a potentially complex matching function for each one is at best tedious and at worst can lead to programming errors.

Many programming languages, Python included, implement a general pattern matching mechanism that is both flexible and efficient: **regular expressions**.

#### Matching

Matching a string against some pattern is done with the `re` module and most typically with the `search()` function in that module. At its very simplest, we can invoke it like this:


```python
import re

if re.search('ab','abba tour'):
  print('a match')
else:
  print('no match')
```

    a match
    

Here we import from `re` the pattern matching function `search()`. This function takes two arguments: a pattern and a string. In this case, the pattern `'ab'` matches any string that contains that letter sequence, e.g. 'abc', 'xab', 'ab', 'xabc'.

We’ll consider the syntax of patterns in depth in the next section, but let’s consider one slightly more complex pattern here: `'a.*b'`. This matches a string that contains 'a' followed anywhere by a 'b'. You can see this by playing with the following program:


```python
import re

if re.search('a.*b','Alice went to Barbados'):
  print('a match')
else:
  print('no match')
```

    a match
    

The `search()` function actually does not return `True` or `False`, but rather a *match* object if the string matches or `None` if it does not. The reason why the code in the two programs above works is that in an `if` statement, a match object will evaluate to `True` and a `None` object will evaluate to `False`. The following code shows this clearly.


```python
import re

#do two matches
res1 = re.search('a.*b','hat')
res2 = re.search('a.*b','nab')
#evaluate results of both matches
for s,r in [('hat',res1),('nab',res2)]:
    #simple if test
    if r:
        print(s,"matches 'a.*b'")
        print("r is a match object")
    else:
        print(s,"does not match 'a.*b'")
        print("r is None")
    #does the match simply false?
    if r == False:
        print('r == False')
    else:
        print('r != False')
    #is the match a None object?
    if r == None:
        print('r == None')
    else:
        print('r != None')
```

    hat does not match 'a.*b'
    r is None
    r != False
    r == None
    nab matches 'a.*b'
    r is a match object
    r != False
    r != None
    

Here we explicitly save the output of `search()` and compare it against `False` and against `None`.

The interest of this distinction is that a match object does more for us than evaluate to `True`. It is an object with several methods we can make use of: `group()`, `start()`, `end()`, and `span()`.

The `group()` method simply returns the matched part of the string. In the case of a pattern like `'a'`, this will simply return 'a' in the case of a match. In the case of a more interesting pattern like `'a.*b'`, the `group()` method returns the entire string from 'a' to 'b'. The following code exemplifies:


```python
import re

#do a match
res = re.search('a.*b','abba')
#if the match succeeds...
if res:
    #print out what is matching
    print("match: ’",res.group(),"’",sep='')
else:
    print('no match')
```

    match: ’abb’
    

If you try this with different command-line arguments, you’ll see that the `group()` method returns the entire string from 'a' to 'b'.

The `start()`, `end()`, and `span()` methods return the starting and ending indices of the matched portion. The `span()` method returns both. The following code exemplifies:


```python
import re

#do a match
res = re.search('a.*b','abba')
#if the match succeeds...
if res:
    #print out what is matching
    print("match: ’",res.group(),"’",sep='')
    print('starting index:',res.start())
    print('ending index:',res.end())
    print('both indices:',res.span())
else:
    print('no match')
```

    match: ’abb’
    starting index: 0
    ending index: 3
    both indices: (0, 3)
    

Notice that, as with expressions with `:`, the ending index is the index of the character after the final character of the pattern.

These methods allow us to see some other aspects of the code. First, the match begins at the earliest possible point in the string. In the case at hand, if there are multiple instances of 'a', the match begins with the first one. Second, the match is as greedy as possible. If there are multiple instances of 'b', the match uses the rightmost one.

Another useful general matching function is `findall()`. What this does is return all instances of the match in a string. For example, if you match 'a' against 'abracadabra', this will return `['a','a','a','a','a']`. The following code exemplifies:


```python
import re

#find all matches
res = re.findall('a','hat')
#if it succeeds, if there is at least 1
if res:
    #print the list
    print('match:',res)
else:
    #print the empty list
    print('no match:',res)
```

    match: ['a']
    

Note that in the event of no match, `findall()` returns an empty list rather than `None`.
