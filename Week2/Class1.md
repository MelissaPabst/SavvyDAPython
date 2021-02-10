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
Feel free to do whatever you prefer when you are comfortable with direct imports like this. 