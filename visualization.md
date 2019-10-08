
# Visualization

## Matplotlib

Matplotlib is a Python 2D plotting library which produces publication quality figures in a variety of hardcopy formats and interactive environments across platforms. Matplotlib can be used in Python scripts, the Python and IPython shell, the jupyter notebook, web application servers, and four graphical user interface toolkits. (https://matplotlib.org/index.html)

Documentation: https://matplotlib.org/contents.html

To install: `pip install matplotlib`


```python
import matplotlib
```

### Simple Plots


```python
import matplotlib.pyplot as plt
```


```python
# X and Y - the coordinates
X = [3,   5, 1.2,   1.9, 3, 6, 4, 5.5, 6.2, 7.2, 9, 9.1]
Y = [3.2, 1,   3.8, 2.5, 1.4, 1.2, 4, 3, 2, 2, 5, 4.3]

plt.plot(X, Y) # drawing the plot -- joining the dots with X and Y coordinates
plt.show()
```


![png](output_7_0.png)


We could also draw a scatterplot with the labels for x-axis and y-axis and the name of the plot.


```python
plt.scatter(X,Y)  # drawing the dots
plt.title("Just dots")
plt.xlabel("x-axis")
plt.ylabel("y-axis")
plt.show()
```


![png](output_9_0.png)


We could also set the limits for the x-axis and the y-axis:


```python
plt.scatter(X, Y)
plt.xlim(0,4)
plt.ylim(0,2.7)
plt.show()
```


![png](output_11_0.png)


When we draw the dots, additionally to the coordinates in `plt.scatter()`, we could set some parameters:

+ s: the size of the dot, 20 by default;
+ c: colour, 'b' for blue by default;
+ marker: the symbol for the dot, 'o' for circle by default.

The list of all [the colour choices](https://matplotlib.org/examples/color/named_colors.html) and the list of all [the markers](https://matplotlib.org/examples/lines_bars_and_markers/marker_reference.html). 

Below are some popular choices for the markers:

+ "." – point
+ "o" – circle
+ "v" – triangle_down
+ "^" – triangle_up
+ "<" – triangle_left
+ ">" – triangle_right
+ "8" – octagon
+ "s" – square
+ "p" – pentagon
+ "P" – plus (filled)
+ "D" – diamond
+ "h" – hexagon

Some popular choices for the colours:

+ 'b' / 'blue'
+ 'g' / 'green'
+ 'r' / 'red
+ 'c' / 'cyan'
+ 'm' / 'magenta'
+ 'y' / 'yellow'
+ 'k' / 'black'
+ 'w' / 'white'

You can use quite exotic colours like 'plum' and 'orchid' from [the xkcd list](https://xkcd.com/color/rgb/), you can also use colours coded in RGB/RGBA format ('#0F0F0F' и '#0F0F0F0F' respectively), as in HTML and CSS.


```python
plt.scatter(X, Y, s=[20, 40, 60, 40, 60, 10], c='aqua', marker='^')
plt.show()
```


![png](output_13_0.png)


You can define colours and sizes as sets:


```python
size = [60, 70, 80, 90, 100, 130]
colors = ['lightsteelblue', 'fuchsia', 'mediumseagreen', 'mediumspringgreen', 'yellow', 'palegreen']
plt.scatter(X, Y, s=size, c=colors, marker='^')
plt.show()
```


![png](output_15_0.png)


What if you want to use a different marker for every dot? The `marker` parameter, unlike `c` and `s`, can't be a set, but you can always set up a loop:


```python
markers = ['h', '*', '8', 'd', '^', 'p', 'h', '*', '8', 'd', '^', 'p']

for x, y, m in zip(X, Y, markers):
    plt.scatter([x],[y],marker=m,s=100)
plt.show()
```


![png](output_17_0.png)


On the `zip(iterables)` function: make an iterator that aggregates elements from each of the iterables.

Returns an iterator of tuples, where the i-th tuple contains the i-th element from each of the argument sequences or iterables. The iterator stops when the shortest input iterable is exhausted. With a single iterable argument, it returns an iterator of 1-tuples. With no arguments, it returns an empty iterator.


```python
x = [1, 2, 3]
y = [4, 5, 6]
zipped = zip(x, y)
list(zipped)
```




    [(1, 4), (2, 5), (3, 6)]




```python
x = [1, 2]
y = [4, 5, 6]
zipped = zip(x, y)
list(zipped)
```




    [(1, 4), (2, 5)]



To label the dots:


```python
dots = ["Lisa", "Anna", "Dina", "Alina", "Lera", "Tatiana", "Polina", "Shaza", "Sarah", "Kenan", "Manuel", "Lisa"]

for x, y, m, d in zip(X, Y, markers, dots):
    plt.scatter(x, y, marker=m, s=100)
    plt.text(x+0.1, y+0.1, d) # +0.1 - to display the text a little bit higher to the right of the dot
plt.show()
```


![png](output_22_0.png)


If you want to display a line alongside the dots, you can use `plot`, if you want to mark just some of the dots, use the `markevery` parameter.



```python
plt.plot(range(10), linestyle='--', marker='D', c='xkcd:mint', markevery=[5, 6,7])
plt.show()
```


![png](output_24_0.png)



```python
plt.plot(range(10), '--gD', markevery=[5,6,7])
plt.show()
```


![png](output_25_0.png)


You can save any plot as a picture using one of the following formats: emf, eps, pdf, png, ps, raw, rgba, svg, svgz.


```python
dots = ["Lisa", "Anna", "Dina", "Alina", "Lera", "Tatiana", "Polina", "Shaza", "Sarah", "Kenan", "Manuel", "Lisa"]

for x, y, m, d in zip(X, Y, markers, dots):
    plt.scatter(x, y, marker=m, s=100, c='xkcd:mint')
    plt.text(x+0.1, y+0.1, d) # +0.1 - to display the text a little bit higher to the right of the dot
plt.savefig('plot1.pdf')
```


![png](output_27_0.png)



```python
plt.plot(range(10), '--gD', markevery=[5,6,7])
plt.savefig('plot2.pdf', dpi=300)#dots per inch parameter to get better quality
```


![png](output_28_0.png)


### ggplot

You don't have to set every parameter manually, you can use pre-made styles for plots. One of the styles is `ggplot`.

Let's take two lists of dots - with (X, Y) coordinates and with (X2, Y2) coordinates:


```python
X2 = [i*2 for i in X]
Y2 = [i*1.5 for i in Y]
X3 = [i*0.5 for i in X]
Y3 = [i*0.7 for i in Y]
print(X, Y, X2, Y2)
```

    [3, 5, 1.2, 1.9, 3, 6, 4, 5.5, 6.2, 7.2, 9, 9.1] [3.2, 1, 3.8, 2.5, 1.4, 1.2, 4, 3, 2, 2, 5, 4.3] [6, 10, 2.4, 3.8, 6, 12, 8, 11.0, 12.4, 14.4, 18, 18.2] [4.800000000000001, 1.5, 5.699999999999999, 3.75, 2.0999999999999996, 1.7999999999999998, 6.0, 4.5, 3.0, 3.0, 7.5, 6.449999999999999]
    


```python
from matplotlib import style  # importing styles
style.use('ggplot')  # choosing ggplot style

plt.plot(X,Y)
plt.plot(X2, Y2)
plt.plot(X3, Y3)

plt.title('Using ggplot')
plt.ylabel('Y-axis')
plt.xlabel('X-axis')

plt.show()
```


![png](output_31_0.png)


You can play with different parameters:


```python
plt.plot(X, Y,'g',label='green line', linewidth=5) #changing the colour and the width of the line
plt.plot(X2, Y2,'c',label='blue line',linewidth=3)

plt.title('Using ggplot')
plt.ylabel('Y-axis')
plt.xlabel('X-axis')

plt.legend()

plt.grid(True,color='orchid')  #changing the parameters of the grid

plt.show()
```


![png](output_33_0.png)


A new data set for a **bar plot**:


```python
X = [1, 2, 3, 4, 5]
Y = [11, 12, 13, 14, 15]

X2 = [6, 7, 8, 9, 10]
Y2 = [15, 14, 13, 12, 11]
```


```python
plt.bar(X, Y)
plt.bar(X2, Y2, color='y')
plt.show()
```


![png](output_36_0.png)


There are a lot of fantastic libraries and packages for creating plots, diagrams, networks etc. Some of my favourite ones: `seaborn`, `plotly` (https://habr.com/company/ods/blog/323210/), `NetworkX` (https://networkx.github.io/documentation/stable/tutorial.html).
