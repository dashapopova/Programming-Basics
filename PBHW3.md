

```python
from operator import itemgetter
from itertools import dropwhile
from string import punctuation
```

1. #### Tokenizing -- 2.5 points

Tokenizing. This is one of the most common (and vexing) operations when processing data.  There is no single correct way to do it.  The correct method will depend on the task at hand.  This problem is designed to give you a sense for the challenges and the possibilities. Give it some thought, but don't go overboard.  We'll soon have additional techniques for defining good tokenizers.


```python
def tokenize(s):
    """Break str s into a list of strings according to some procedure 
    tailored for the task at hand."""

    #your code
    return #specify the output of the function
```

2. #### Word counts -- 2.5 points

Download this file to your computer and make sure it is in the same
directory/folder as this homework file:
https://github.com/dashapopova/Programming-Basics/blob/master/alice.txt
Open alice.txt in your text editor and study its composition. Clearly,
we would need to do a lot of special processing of this file in order
to get accurate word counts for Alice.  However, for this problem, you
need to make only a minimal effort:

Complete `gutenberg_file_wc` so that it can read in the file alice.txt 
and tokenize only the lines that occur between the two lines from the 
file that start this way:
```
*** START OF THIS PROJECT GUTENBERG EBOOK
*** END OF THIS PROJECT GUTENBERG EBOOK
```
There are a lot of strategies for doing this.  The one that is
NOT ALLOWED is deleting material from alice.txt and saving the
result.  Your function has to work without any modifications to 
alice.txt.

A hint: you can try doing this:
```
alice = open('alice.txt').read()
a = alice.find("*** START OF THIS PROJECT GUTENBERG EBOOK") 
z = alice.find("*** END OF THIS PROJECT GUTENBERG EBOOK") 
alice_new = alice[a:z]
```


```python
def gutenberg_file_wc(filename):
    """Open the file with name filename, tokenize it with your 
    tokenize function, and return a dict mapping words to their 
    counts in the file.  Tokenize only the material that occurs
    between the two lines given above."""
    #insert your code here
    return #the output of the function
print(gutenberg_file_wc('alice.txt'))#testing the function
```

3. #### Counts by year -- 2.5 points 

The raw data files for the Google Books collection are available for 
download. The files are huge, so I created a sample. Download this 
file to your computer and make sure it is in the same directory/folder 
as this homework file:
https://github.com/dashapopova/Programming-Basics/blob/master/googlebooks.txt

The format of this file is as follows (whitespace inserted for 
readability):
```
word TAB year TAB match_count TAB volume_count NEWLINE
```

The TAB character is `\t`, which you can treat like any other (for
example, you can split a string on `\t`).

Your task: complete `googlebooks_counts_by_year` so that it processes
my sample file and returns a 2d dictionary with this structure:
```
{
  word1: {year1: count, year2: count ...},
  word2: {year1: count, year2: count ...},
  ...
}
```
where the nature of the year dicts is determined by the file.
(That is, different words will have different years and counts
associated with them.)


```python
def googlebooks_counts_by_year(filename):
    """Maps a Google books 1-grams file to a 2d dictionary
    giving each word's counts by year."""

    #insert your code here     
    return #specify the output of your function
print(googlebooks_counts_by_year('googlebooks.txt'))#testing the function
```

4. #### Collapse by year -- 2.5 points

Complete the function `googlebooks_year_collapse` so that it takes
as input the output of `googlebooks_counts_by_year` and collapses
it down so that each word is associated with its single tokencount
for the full, obtained by summing up all of the counts for the
years associated with that word. 


```python
def googlebooks_year_collapse(d):
    """Convert the output of googlebooks_counts_by_year to 
    a simpler dict mapping words to counts."""
    #your code should be here
    return #the output of the function
print(googlebooks_year_collapse(googlebooks_counts_by_year('googlebooks.txt')))#testing the function
```
