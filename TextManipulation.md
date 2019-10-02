
## Manipulating text

The simplest function for manipulating text is `sub()` in the `re` module. This
function converts one string into another by pattern matching: whatever part of the string matches the specified pattern is replaced with the specified replacement.
The function takes those three arguments plus two more: a pattern, a replacement,
the string, and the maximum number of replacements `count` plus additional flags
`flags`. Here is a simple example:


```python
import re
#define a string
s1 = 'This is a rather long string'
#replace ’.s’ with ’WOW’
s2 = re.sub('.s','WOW',s1)
#print old and new strings
print(s1,'\n',s2)
```

    This is a rather long string 
     ThWOW WOW a rather longWOWtring
    

We can see the `count` variable at work in the next example:


```python
import re
#a test string
s1 = 'This is a rather long string'
#a pattern
pat = '.s'
#find how many instances of the pattern
countmax = len(re.findall(pat,s1))
#print the string
print(s1)
#make that many substitutions 1 by 1
i = 1
while i < countmax+1:
    #make a change
    s2 = re.sub(pat,'WOW',s1,count=i)
    #print that one change
    print('\t',i,':',s2)
    #increment counter
    i += 1
```

    This is a rather long string
    	 1 : ThWOW is a rather long string
    	 2 : ThWOW WOW a rather long string
    	 3 : ThWOW WOW a rather longWOWtring
    

Here, we identify how many instances of the pattern there are with `findall()` and we then iterate through making different numbers of substitutions. Note that when `count = 0`, we make all the substitutions, rather than none of them.

Finally, the `flags` argument allows for a number of options. The only one you’re
liable to use is case-insensitive matching when `flags=re.I`. Here’s an example:


```python
import re
#a test string
s1 = 'This is a rather long string'
#do a replacement
s2 = re.sub('t','WOW',s1)
#do a case-insensitive replacement
s3 = re.sub('t','WOW',s1,flags=re.I)
#incorporate case directly in the pattern
s4 = re.sub('t|T','WOW',s1)
#show all three results
print(s1,'\n',s2,'\n',s3,'\n',s4,sep='')
```

    This is a rather long string
    This is a raWOWher long sWOWring
    WOWhis is a raWOWher long sWOWring
    WOWhis is a raWOWher long sWOWring
    

Notice here how the effect of case-insensitive matching can be achieved by adjusting
the pattern instead.

If your substitutions are all converting single letters to other single letters you can
make use of the efficient `translate()` string method. You first make use of the
`str.maketrans()` method to make a *translation table*; you then use that table to
make the translation. Here’s an example:


```python
#make a translation table
mytab = str.maketrans('aeiou','happy')
#a test string
s = 'This is my sample string'
#print that string
print(s)
#print the translation
print(s.translate(mytab))
```

    This is my sample string
    Thps ps my shmpla strpng
    

A translation table is implemented as a Python dictionary. Note that the two string
arguments to `str.maketrans()` must be the same length.


```python
print(type(mytab))
```

    <class 'dict'>
    

Another function that is quite useful is `re.split()`. Recall the string method
`split()` which splits a string up based on some specific delimiter string. The
`re.split()` function allows you to split a string based on a regular expression
instead. Here’s an example:


```python
import re
#a test string
s = 'First sentence. Second sentence.'
#do a regular split
ss1 = s.split('e.')
#do re.split
ss2 = re.split('e.',s)
#print the sentence
print(s)
#print split() results
print('s.split()')
for ss in ss1:
    print('\t"',ss,'"',sep='')
#print re.split() results
print('re.split()')
for ss in ss2:
    print('\t"',ss,'"',sep='')
```

    First sentence. Second sentence.
    s.split()
    	"First sentenc"
    	" Second sentenc"
    	""
    re.split()
    	"First s"
    	"t"
    	"c"
    	" S"
    	"ond s"
    	"t"
    	"c"
    	""
    

Here we invoke the string method `split()` and `re.split()` with the string
'e.'. The string method `split()` interprets this literally and splits the string
into three strings; `re.split()` interprets this as a regular expression and splits
the string into eight strings. Note too that the syntax for these is different. The
`re.split()` function takes two arguments where the string to split is the second
argument. The `split()` method is instead suffixed to the string it operates on
and takes a single argument.

Finally, we have the string method `join()` which joins a set of strings together
with string infix. The syntax is a bit unintuitive. The string it is suffixed to is the
infix. It takes a single argument which is a list of strings. Here’s a simple example:


```python
#a test sentence
s = 'This is a sentence.'
#split it into words
wds = s.split()
#define hyphen
hyphen = '-'
#join bits with hyphen
hyphenated = hyphen.join(wds)
#print original sentence
print(s)
#print hyphenated sentence
print(hyphenated)
```

    This is a sentence.
    This-is-a-sentence.
    
