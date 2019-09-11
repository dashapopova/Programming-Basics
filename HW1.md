## Homework 1 Assignment

Please e-mail an .ipynb file or a link to an .ipynb file in your github repository to daschapopowa@gmail.com by noon, September 18th.

1. **Datatypes: 2 points**

Find a datatype that we have not discussed in class (don't forget to tell me what it is). List at least three functions that one could apply to the datatype you found.

An example solution:
datatype: `list`
+ `x.append()` – this method adds an element at the end of the list `x`
+ `x.pop(1)` – this method removes an element at a specified index position in the list `x` (1 in this case). The method returns that element, altering the list at the same time
+ `len(x)` -- this function is used to determine the length of the list `x`

2. **Comparisons: 2 points**

What do the following numeric comparisons mean when they are applied to strings?
+ `==`
+ `!=`
+ `>`
+ `>=`
+ `<`
+ `<=`

A hint: `’flower’ < ’zebra’` precedes alphabetically

3. **Semitic morphology: 2 points**

Semitic morphology involves intercalating vowels and consonants to express morphological categories.
For example, the Arabic root *k,t,b* occurs in at least the following forms: *katab-a* ’he
wrote’, *kaatab-a* ’he corresponded’, *kutib-a* ’it was written’, *kitab* ’book’, *kuttaab* ’writers’, *uktub*
’write!’, etc.
How might you use `format()` to describe this system? Give a sample representation for the
root *k,t,b* and how `format()` could be used to express different categories.

4. **Pragmatics: 2 points**
```
x = ’The bartender... absolutely horrible... we waited 10 min before we even got her attention...
and then we had to wait 45 – FORTY FIVE! – minutes for our entrees... stalk the waitress to
get the cheque... she didn’t make eye contact or even break her stride to wait for a response ...’
```
What will happen if we apply `lower()` to the string `x`?
What information will we lose when `lower()` is applied to `x`?
List one linguistic task where the application of `lower()` to `x` is useful and one task where it
is harmful.

5. **Funky Dictionary: 2 points**

List commands that would do the following:
+ create a dictionary `d` that contains 10 Russian (slang) words that, you think, a
non-native speaker of Russian might not know with definitions in English;
+ test that your dictionary contains 10 pairs;
+ test whether a given key is in the dictionary;
+ delete an entry (a key-value pair);
+ add an entry;
+ print a list of keys;
+ print a list of values;
+ print a list of key-value pairs.
