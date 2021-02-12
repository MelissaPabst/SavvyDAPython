# pandas

![pandas](pandashi.jpeg)

We're switching gears a bit; NumPy taught us how to do math with ndarrays of single-type data (homogenous) efficiently, and next on our agenda is **pandas**. Pandas is another library for Python and is built on top of NumPy. Pandas is better suited for data of heterogenous types, and data in tables, or **dataframes**, as they call them in pandas. 

Remember MatPlotLib? Well, pandas provides **wrappers** around the matplotlib library, reducing the lines of code needed to use matploblib code. You may recall from your lesson on object-oriented programming the concept of **abstraction**, which aims to hide the bits that aren't needed, effectively reducing the complexity and therefore the lines of code. Well, that's what a wrapper does. You don't need to know how your coffee pot works, but that you can get some hot bean juice if you do x, y, and z steps. A wrapper is like the buttons on the coffee pot. 

Why is it called pandas? I don't mean to de-mystify it, and you can continue to picture in your mind cute little pandas typing away inside your computer, but it comes from *panel data*, an econometrics term you don't hear a lot and is the term for multidimensional structured datasets. (Please stop trying to insert bamboo in your floppy disk drive.)

Pandas has a wide range of capabilities beyond NumPy, especially when it comes to data structures and data manipulations needed to clean and analyze our data, but we'll still be using NumPy here and there. 

Instructions for installation can be found [here](https://pandas.pydata.org/pandas-docs/stable/getting_started/install.html).

And then we start by naming our imports:

```
>>> import pandas as pd
>>> from pandas import Series, DataFrame
```
Whenever you see pd, we are referring to the pandas library. I also imported Series and Dataframe into the local namespace because they are frequently used, and now I can call them directly without typing pd.Series:

```
>>> my_obj = Series([4, 7, -2, -7])
>>> my_obj
0    4
1    7
2   -2
3   -7
dtype: int64
>>> my_obj = pd.Series([2, 5, 8, 3])
>>> my_obj
0    2
1    5
2    8
3    3
dtype: int64
```
Feel free to do whatever you prefer after you are comfortable with direct imports like this.

## Series

What we created above is a **series**, which is a 1D array-like object, similar to a NumPy 1D array, but has an associated array of index labels. 

The most basic building of a series looks like this:

``` 
>>> s = pd.Series(data, index=index)
```
And "data" can be a Python dictionary, an ndarray, or even a scalar value. 


Here we have a panda series, with the index labels on the left and the data on the right:

```
>>> my_obj = pd.Series([2, 5, 8, 3, 1, 0])
>>> print(my_obj)
0    2
1    5
2    8
3    3
4    1
5    0
dtype: int64
```
Here is one made from a NumPy array: 

```
>>> import numpy as np
>>> np_series = pd.Series(np.random.randn(5))
>>> np_series
0    2.518028
1    1.018381
2   -0.488189
3   -0.249349
4   -0.166437
dtype: float64
```
Here is a series from a python dictionary:

```
>>> dict = {"r": 2, "d": 2, "c": 3, "p": 0}
>>> dict_series = pd.Series(dict)
>>> dict_series
r    2
d    2
c    3
p    0
dtype: int64
```

The default index label starts at 0, and goes up to length - 1, but we can specify the label should we choose by supplying "index = ". Note: index must be the same length as the data. 
 
```
 >>> labeled_obj = pd.Series([4, 6, -1, -2], index = ['m', 'e', 't', 'q'])
>>> print(labeled_obj)
m    4
e    6
t   -1
q   -2
dtype: int64
```
When we create a series from a scalar value, the value repeats to the size of the provided index. 

```
>>> pd.Series(5, index=["a", "b", "c", "d", "e"])
a    5
b    5
c    5
d    5
e    5
dtype: int64
```


We can call the **index** and **values** attributes of each array object we created:

```
>>> my_obj = pd.Series([2, 5, 8, 3, 1, 0])
>>> my_obj.values
array([2, 5, 8, 3, 1, 0])
>>> my_obj.index
RangeIndex(start=0, stop=6, step=1)


>>> labeled_obj = pd.Series([4, 6, -1, -2], index = ['m', 'e', 't', 'q'])
>>> labeled_obj.values
array([ 4,  6, -1, -2])
>>> labeled_obj.index
Index(['m', 'e', 't', 'q'], dtype='object')
>>> 
```
And just as with NumPy, we can select single values (or a set of values) from the series with indexing:

```
>>> labeled_obj
m    4
e    6
t   -1
q   -2
dtype: int64
>>> labeled_obj['q']
-2
>>> labeled_obj[['q', 'm']]
q   -2
m    4
dtype: int64
>>> my_obj
0    2
1    5
2    8
3    3
4    1
5    0
dtype: int64
>>> my_obj[3]
3
>>> my_obj[[3, 0, 1]]
3    3
0    2
1    5
dtype: int64
```
We can perform mathematical operations, scalar operations, NumPy functions, etc. and the series will preserve the index-value relationship:

```
>>> dict_series * 2
r    4
d    4
c    6
p    0
dtype: int64
>>> dict_series > 1
r     True
d     True
c     True
p    False
dtype: bool
>>> dict_series[dict_series > 1]
r    2
d    2
c    3
dtype: int64
>>> np.mod(dict_series, 2)
r    0
d    0
c    1
p    0
dtype: int64
>>> 
```

 