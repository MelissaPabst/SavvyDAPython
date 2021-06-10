# Plot-Thirsty

I heard the class was plot-thirsty. My recommendation is to read a book or two!

Even book plots have plots...
 
![plotplot](week4images/plotplot.png)
 
Waaaaaaay back in Week 1, Night 4 we introduced Matplotlib. It's okay if you haven't practiced a lot with it. This module should give you a brief overview of a few kinds of common plots so you will be comfortable doing it when the time comes.  

So... I think if you were using Jupyter you can use interactive plotting with:

```
%matplotlib notebook
```
And if not, remember to import it:

```
import matplotlib.pyplot as plt
```
But I do want to mention this module was NOT created with Jupyter, so there might be differences in commands. 

## Simple line plot

For a quick warm-up, let's plot a simple Numpy line:

```
>>> data = np.arange(10)
>>> data
array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])
>>> plt.plot(data)
[<matplotlib.lines.Line2D object at 0x11f39e100>]
>>> plt.show()
```
![numpyline](week4images/numpyline.png)

## Figure Objects

Plots within Matplotlib reside within a "Figure" object. 

```
>>> fig = plt.figure()
>>> ax1 = fig.add_subplot(2, 2, 1)
>>> ax2 = fig.add_subplot(2, 2, 2)
>>> ax3 = fig.add_subplot(2, 2, 4)
>>> plt.show()
```
What we've done is create a blank 2 X 2 matplotlib figure (2x2 indicates the figure holds 4 subplots) with three subplots, and we designated each a quadrant position of 1, 2, and 4. 

![basicfig](week4images/basicfig.png)

And when we add a plot to a figure, the plot goes into the last subplot.

```
>>> fig = plt.figure()
>>> ax1 = fig.add_subplot(2, 2, 1)
>>> ax2 = fig.add_subplot(2, 2, 2)
>>> ax3 = fig.add_subplot(2, 2, 4)
>>> plt.plot(np.random.rand(25).cumsum())
[<matplotlib.lines.Line2D object at 0x12cc36ac0>]
>>> plt.show())
```
![subplot4](week4images/subplot4.png)

Let's add to the other subplots. Don't worry about all the parameters and customizations, yet. The objects we created with fig.add_subplot are called "AxesSubplot" objects and you can call methods on their instances. 

```
>>> fig = plt.figure()
>>> ax1 = fig.add_subplot(2, 2, 1)
>>> ax2 = fig.add_subplot(2, 2, 2)
>>> ax3 = fig.add_subplot(2, 2, 4)
>>> plt.plot(np.random.rand(25).cumsum())
[<matplotlib.lines.Line2D object at 0x12dcf11f0>]
>>> ax1.hist(np.random.rand(25), bins=20, color='k', alpha=0.3)
(array([1., 2., 0., 4., 1., 1., 2., 3., 0., 1., 1., 0., 0., 1., 2., 1., 1.,
       2., 0., 2.]), array([0.04311005, 0.09065546, 0.13820087, 0.18574628, 0.23329169,
       0.2808371 , 0.32838252, 0.37592793, 0.42347334, 0.47101875,
       0.51856416, 0.56610957, 0.61365498, 0.66120039, 0.7087458 ,
       0.75629121, 0.80383663, 0.85138204, 0.89892745, 0.94647286,
       0.99401827]), <BarContainer object of 20 artists>)
>>> ax2.scatter(np.arange(25), np.arange(25) + 5)
<matplotlib.collections.PathCollection object at 0x12dcf1430>
>>> plt.show()
```
![fullfigure](week4images/fullfigure.png)

So now we have a histogram, a scatter plot, and a line plot. 

Additionally, we can create a figure without defining the subplot objects: 

```
>>> fig, axes = plt.subplots(2,3)
>>> axes
array([[<AxesSubplot:>, <AxesSubplot:>, <AxesSubplot:>],
       [<AxesSubplot:>, <AxesSubplot:>, <AxesSubplot:>]], dtype=object)
>>> plt.show()
```
![no objects](week4images/noobjects.png)

It's kinda scrunchy, so I'd recommend adjusting the spacing with subplots\_adjust: 

It takes the params left, bottom, right, top, wspace, and hspace. 

An example:
plt.subplots_adjust(left=0.125,
                    bottom=0.1, 
                    right=0.9, 
                    top=0.9, 
                    wspace=0.2, 
                    hspace=0.35)
                    
wspace and hspace specify the space reserved between Matplotlib subplots. They are the fractions/percentages of axis width and height, respectively.

left, right, top and bottom parameters specify four sides of the subplots’ positions. They are the fractions of the width and height of the figure.

This will remove all whitespace between the plots: 

```
# create our figure
>>> fig, axes = plt.subplots(2,3)
# plot all six with a function
>>> for i in range(2):
...     for j in range(3):
...             axes[i,j].hist(np.random.randn(250), bins=50, color='k', alpha=0.5)
... 
# set percentages to 0
>>> plt.subplots_adjust(wspace=0, hspace=0)
>>> plt.show()
```
![no spacing](week4images/nospacing.png)

How you space your subplots is up to you and will depend on the situation.

We used bins with [histogram plotting](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.hist.html)... I don't want to gloss over it:

If bins is an integer, it defines the number of equal-width bins in the range.

If bins is a sequence, it defines the bin edges, including the left edge of the first bin and the right edge of the last bin. 

And alpha was to adjust the transparency. Matplotlib allows you to adjust the transparency of a graph plot using the alpha attribute.

By default, alpha=1

If you want to make the graph plot more transparent, then you can make alpha less than 1, such as 0.5 or 0.25.

If you want to make the graph plot less transparent, then you can make alpha greater than 1. This solidifies the graph plot, making it less transparent and more thick and dense, so to speak.

# Styles

All the ins and outs of styling your plots can be found [here](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.plot.html)

**Colors**: Some color abbreviations are provided for common colors('g' is green, 'k' is black, 'b' is blue, 'r' is red, etc.), but any color is available through a [HEX code](https://imagecolorpicker.com/en). 

**Markers**: This is the little mark you use to mark a data point. There are many markers in the documentation.

**Line styles**: Lines are how we connect the markers, and below are the options. 

![line styles](week4images/linestyles.png)

The convention for declaring a style is as follows:

**fmt = '[marker][line][color]'**
 
So if we wanted green circles with a straight line, it would look like "o-g".

And when we go to use that in our plot, with y versus x:

ax.plot(x, y, 'o-g")

or 

ax.plot(x, y, linestyle='solid', color='g', marker='o')

```
>>> plt.plot(np.random.randn(25).cumsum(), 'o-g')
[<matplotlib.lines.Line2D object at 0x139e925b0>]
>>> plt.show()
```
And now we have a plot with green circles, connected with solid lines:

![the og](week4images/theog.png)

## Ticks and Labels and Legends, oh my! (And titles!)

xlim: controls x plot range
ylim: controls y plot range

Calling plt.xlim() would return the current x-axis plotting range, while calling plt.xlim([1, 10]) sets the x-axis range of 1-10. 

Discuss... What is a **tick**???

xticks/yticks: Use set\_xticks/set\_yticks to tell matplotlib where to place ticks.

xticklabels/yticklabels: We can label the ticks with set\_xticklabels or set_yticklabels.

```
>>> fig = plt.figure()
>>> ax = fig.add_subplot(1, 1, 1)
>>> ax.plot(np.random.rand(2000).cumsum())
[<matplotlib.lines.Line2D object at 0x134e5eee0>]
>>> ticks = ax.set_xticks([0, 500, 1000, 1500, 2000])
>>> labels = ax.set_xticklabels(['zero', '5-hundo', 'a grand', '1.5 grand', '2 grand'])
>>> ax.set_title('We made a plot with some ticks, labels, and title!')
Text(0.5, 1.0, 'We made a plot with some ticks, labels, and title!')
>>> ax.set_xlabel('PROFIT')
Text(0.5, 0, 'PROFIT')
>>> plt.show()
```
With a little code, we can make something look like this: 

![PROFIT](week4images/PROFIT.png)

If we plot multiple trends on the same subplot, we might want a legend to distinguish the lines. Use ax.legend(). 

```
>>> fig = plt.figure()
>>> ax = fig.add_subplot(1, 1, 1)
>>> ax.plot(np.random.rand(50).cumsum(), 'b', label='uno')
[<matplotlib.lines.Line2D object at 0x1469aa0a0>]
>>> ax.plot(np.random.rand(50).cumsum(), 'g--', label='dos')
[<matplotlib.lines.Line2D object at 0x1469aa400>]
>>> ax.plot(np.random.rand(50).cumsum(), 'or', label='tres')
[<matplotlib.lines.Line2D object at 0x1469aa790>]
>>> ax.legend(loc='best')
<matplotlib.legend.Legend object at 0x14699ff10>
>>> plt.show()
```

![legendary](week4images/legendary.png)


If you ever want to save a plot, you can do it like this: 

```
>>> plt.savefig('legendary.svg')
# or 
>>> plt.savefig('legendary.pdf')
```
Of course, there are options for saving if you look in the documenation


Your data set will dictate how you dress and design your plots. See documentation for more possibilities. Heck, there are glorious--GLORIOUS--tutorials out there! If it's something you can do in Excel or Tableau, I'm willing to bet there is a way to do it with Matplotlib or another plotting library, such as Seaborn. 

[Here are some tutorials to try](https://matplotlib.org/stable/tutorials/index.html), as well as a bunch of [example plots](https://matplotlib.org/stable/gallery/index.html) to inspire you. Challenge yourself to do at least 3 that appeal to you! Share your results with your classmates. Let's see who can come up with some funky plots. 


## Popular Plots with Pandas 

We use **.plot()** on a DataFrame (or Series!) and borrow plt.show() from Matplotlib.

.plot() has several optional parameters. Most notably, the "kind" parameter accepts eleven different string values (default is kind="line") and determines which kind of plot you’ll create:

"area" is for area plots.
"bar" is for vertical bar charts.
"barh" is for horizontal bar charts.
"box" is for box plots.
"hexbin" is for hexbin plots.
"hist" is for histograms.
"kde" is for kernel density estimate charts.
"density" is an alias for "kde".
"line" is for line graphs.
"pie" is for pie charts.
"scatter" is for scatter plots.

A common syntax to draw a plot from a DataFrame is like this:

df.plot(x="x column", y="y column", kind="line")


### Scatter Diagram

Scatter plots are used to depict a relationship between two variables.

```
>>> data = {'Acceleration_Rate': [1.2, 1.34, 1.22, 1.56, 3.0, 2.55, 1.1, 1.21],
... 'Speed': [34, 64, 77, 22, 86, 56, 44, 21]}
>>> df = pd.DataFrame(data, columns=['Acceleration_Rate', 'Speed'])
>>> df.plot(x = 'Acceleration_Rate', y = 'Speed', kind='scatter')
<AxesSubplot:xlabel='Acceleration_Rate', ylabel='Speed'>
>>> plt.show()
```
I don't really see any correlation between the data here, do you? 

![scattered](week4images/pandasscatter.png)

### Line

Line charts are often used to display trends. We'll use time for an example.

Let's see how much better we got at fishing: 

```
>>> data = {'Year': [2010, 2011, 2012, 2013, 2014, 2015, 2016, 2017, 2018, 2019],
... 'Fish_Caught': [45, 42, 55, 33, 65, 77, 54, 88, 102, 213]}
>>> df = pd.DataFrame(data, columns=['Year', 'Fish_Caught'])
>>> df.plot(x='Year', y='Fish_Caught', kind='line')
<AxesSubplot:xlabel='Year'>
>>> plt.show()
```
Dang! I would have thought fishing would have been a pandemic-safe hobby, but we didn't go in 2020. 

![fishing](week4images/fish.png)

Note: As an alternative to passing strings to the "kind" parameter of .plot(), DataFrame objects have several methods that you can use to create the various kinds of plots described above:

.area()

.bar()

.barh()

.box()

.hexbin()

.hist()

.kde()

.density()

.line()

.pie()

.scatter()

### Histogram

So, for a [histogram](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.plot.hist.html), which gives us an overview of our dataset and is a representation of the distribution of data, we could do the following:

```
>>> plt.show()
>>> df = pd.DataFrame(data, columns=['Year', 'Fish_Caught'])
>>> ax = df.plot.hist(bins=10, alpha=0.5)
>>> plt.show()
```
![fishhist](week4images/fishhist.png)

```
>>> df = pd.DataFrame(data, columns=['Year', 'Fish_Caught'])
>>> df.hist(bins=10, alpha=0.5)
array([[<AxesSubplot:title={'center':'Year'}>,
        <AxesSubplot:title={'center':'Fish_Caught'}>]], dtype=object)
>>> plt.show()
```

![fishhist2](week4images/fishhist2.png)

Notice the difference between df.hist() and df.plot.hist(). They do different things; df.hist() will produce a separate plot for each Series while df.plot.hist() will produce a stacked single plot.

So there are df.whatever\_plot() methods and there are df.plot.whatever\_plot() methods. Pay attention to ensure you use the one you intend to use. (Hint: Use which one is more useful!).

### Bar Chart

Number of fish caught per year in bar format:

```
>>> ax=df.plot.bar(x='Year', y='Fish_Caught')
```
![fishbar](week4images/fishbar.png)


### Pie Chart

Fish pie, anyone?

```
>>> data = {'Year': [2010, 2011, 2012, 2013, 2014, 2015, 2016, 2017, 2018, 2019],
... 'Fish_Caught': [45, 42, 55, 33, 65, 77, 54, 88, 102, 213]}
>>> df = pd.DataFrame(data, index=[2010, 2011, 2012, 2013, 2014, 2015, 2016, 2017, 2018, 2019])
>>> ax = df.plot.pie(y='Fish_Caught', figsize=(5,5))
>>> plt.show()
```
![fishpie](week4images/fishpie.png)

Not too difficult. 

And you can always plot subsets of data, etc. Whatever you'd like. Just make sure to refer to the documentation, always!

# Seaborn
