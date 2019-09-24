# On Functions

### Back to the school math:

f(x) = x + 2, x is the argument of f(x), a variable of type, let's say, integer or float.

If we specify the value of x, e.g.:

* x = 2, then 2 will be put in the x slot: f(2) = 2 + 2
* x = 3, then 3 will be put in the x slot: f(3) = 3 + 2
* x = 'dasha', then f(x) won't be computed, since x is not an integer or float.

### Now:

we define functions that take arguments of a certain type, e.g., the `mean(vals)` function will take any list that we give it when we invoke it and put it in the `vals` argument slot, the `tokenize(s)` function will take any string that we supply when we invoke the function and put it in the `s` slot. For example:

```python
#a function LENGTH that takes an argument s (s is like x in the math example above, it just signals that our function needs an argument)
def length(s):
  #and returns the length of any argument that the function will be given
  return len(s)

#a concrete value that we want our function to work on
s_value = ’hats and lemons’  
#now we want to print the result of the application of the function LENGTH to a concrete argument s_value = 'hats and lemons'
print(length(s_value))
```
As in the math example, where 2, 3 replaced x, `s_value` will automatically replace `s` and our function `length(s)` will compute the length of `s_value`.
