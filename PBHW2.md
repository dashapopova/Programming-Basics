
## Homework Assignment 2

##### Due Sept 25th, at noon

1. **CVC syllables generator -- 1 point** 

Write a program that generates CVC syllables using `vowels = 'aeiou'` and `consonants = 'ptkbdg'`, but excludes cases where the two consonants are the same. That is, we do not want items like *dod* or *bab*.

2. **Define a proper title case function -- 1 point**

Try to do a better job of getting title case.  For example, "the cat in the hat".title() ==> "The Cat In The Hat", but we want "The Cat in the Hat" 


```python
def proper_title_case(s):
    nocaps = ["the", "in", "on", "a", "an"] # This needs to be extended.
    #Your code goes below this comment
    return #here goes what you want the function to return
print(proper_title_case('An ant on a table'))#to test your function
print(proper_title_case('The Cat In the Hat'))#to test your function
```

3. **Write the function `mean` -- 1 point**

Complete the function `mean` for calculating the mean (average) of a 
list of numeric values.  Your function should take a list `vals` as its 
argument and return a float.  Keep in mind that `vals` might contain int 
values.
Consider doing it with the in-line function `sum`, which facilitates a fast and readable one-line version of the function.


```python
def mean(vals):
    """Return the mean of the values in vals, presupposed to be 
    numeric (float, int, or long)."""
    return #here goes what you want the function to return

print(mean([1,5,1.1]))#to test your function
```

4. **Write the function `standard deviation` -- 1 point**

Complete the function `sd` for calculating the standard deviation of a 
list of numeric values.  Your function should take a list `vals` as its 
value and return a float.  Keep in mind that `vals` might contain int 
values. For details on calculating the standard deviation, see
http://en.wikipedia.org/wiki/Standard_deviation

I suggest using `float(len(vals)-1)` for the denominator, but 
`float(len(vals))` is fine.
To get the square root of a float `x`, use `math.sqrt(x)`


```python
import math

def sd(vals):
    """Return the standard deviation of the values in vals, 
    presupposed to be numeric (float, int)."""
    #Your code goes below this comment, use the mean fuction defined in the previous task
    return #here goes what you want the function to return

print(sd([0,1,2]))#to test your function
```

5.1. **Basic CSV parser -- 2 points**. 

Complete the following function for turning the str 
`myspreadsheet` into a 10x3 matrix of data.  I should emphasize that the 
top line of `myspreadsheet` is not part of the data.  It's just there to 
help us out.
Column 0 of your data should be int values.
Column 1 of your data should be float values.


```python
myspreadsheet ="""Subject,Height,Occupation
1,74.37000326528938,Psychologist
2,67.49686206937491,Psychologist
3,74.92356434760966,Psychologist
4,64.62372198999978,Psychologist
5,67.76787900026083,Linguist
6,61.50397707923559,Psychologist
7,62.73680961908566,Psychologist
8,68.60803984763902,Linguist
9,70.16090500135535,Psychologist
10,76.81144438287173,Linguist"""

def csv_parser(s):
    """Parses the string s into lines, and then parses those lines by
    splitting on the comma and converting the numerical data to int.
    The output is a list of lists of subject data."""
    #Your code goes below this comment
    # Data is our output. It will be a list of lists.    

    # Split csv into lines and store them in a list called 'lines'.
    
    # Remove the first element from lines, so that you have only the data lines left.
    
    
    # At this stage, we loop through the list called lines.
    # As you loop
    #     i. split each line on the commas;
    #    ii. convert the Subject variable to int.
    #   iii. convert the Height variable to float.
    #    iv. add to data a list consisting of this line's Subject, Height, and Occupation values 
    
    return #here goes what you want the function to return
print(csv_parser(myspreadsheet))#to test your function
```

5.2. **The mean height -- 2 points**

Complete the following function for computing the mean height of the 
subjects in this data set, using your mean function from above.


```python
def mean_height(data):
    """Return the mean numerical value of column 1 in an list of lists.
    data is the output of csv_parser(myspreadsheet)"""
    #Your code goes below this comment
    return #here goes what you want the function to return
print(mean_height(myspreadsheet))#to test your function
```

5.3. **Occupation distribution -- 2 points**. 

Complete the following function so that it 
returns a dictionary mapping occupation names into the number of times 
they occur in the data.


```python
def occupation_distribution(data):
    """Returns the list of occupations given in column 2 of data.
    data is the output of csv_parser(myspreadsheet)"""
    #Your code goes below this comment
    return #here goes what you want the function to return
print(occupation_distribution(myspreadsheet))#to test your function
```
