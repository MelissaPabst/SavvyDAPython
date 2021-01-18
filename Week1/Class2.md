# NumPy, continued.

## Warmup

We left off talking about the advantages of numpy ndarrays, and tonight we will delve into them further. But let's make sure you have the hang of creating a Numpy ndarray. 

Given the following, create a numpy array:

```
temps = [[[34.5, 65.3], [23.4, 65.0], [99.3, 96.3]],  [[23.4, 54.2], [32.4, 34.2], [12.4, 56.4]]]
```

Create numpy array.
What are its attributes? ndim? shape? size? dtype?

# Indexing and Slicing

In our previous studies, we discussed **indexing**, or how to access subsets of data or elements of data within arrays. 

And remember, indexing begins with zero, so the location of the first item is [0], NOT [1].

One-dimensional arrays allow us to access innermost items with one set of '[]'. This selects an element in a row.

```
>>> banana = np.array([1, 2, 3])
>>> banana[1]
2
```

Two-dimensional arrays require two: '[][]'. This selects a [row] and a [column].

```
>>> a = np.array([[1, 2, 3],
...               [4, 5, 6],
...               [7, 8, 9]])
>>> a[0][1]
2
```

Three-dimensional arrays require three: '[][][]'. This selects a [matrix] a [row] and a [column].

What about four-dimensional arrays?

Let's practice with temps, a three-dimensional array.

```
>>> temps = [[[34.5, 65.3], [23.4, 65.0], [99.3, 96.3]],  [[23.4, 54.2], [32.4, 34.2], [12.4, 56.4]]]
>>> np.array(temps)
array([[[34.5, 65.3],
        [23.4, 65. ],
        [99.3, 96.3]],

       [[23.4, 54.2],
        [32.4, 34.2],
        [12.4, 56.4]]])
>>> 
```

Looking at temps, using indeces, how would we access 23.4?

What is the value at [0][2][1]?
What is the value at [1][2][0]?
What about [0][0][0]?

Keep practicing! 

You can find an explanation of indexing with top-notch visuals [here](https://www.pythoninformer.com/python-libraries/numpy/index-and-slice/#:~:text=Slicing%20an%20array,accessed%20in%20a%20different%20order.)

Let's look at **slicing** ndarrays. When you use slicing techniques, you are creating a **view** of the original array. 

```
>>> apples = np.arange(10)
>>> apples
array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])
>>> apples[2]
2
>>> apples[5:8]
# [5:8] eliminates the first five elements, and shows the values at [6] [7] and [8]
array([5, 6, 7])
```



# Scalar Mathematical Operations

A great thing about arrays is that they allow for batch operations to be carried out in a scalar capacity (meaning we can perform an operation on an array and it will be applied to each element of the array without using for loops). Let's try it out:

```
>>> banana = np.array([1, 2, 3], dtype=np.float64)
>>> print(banana)
[1. 2. 3.]
>>> banana * 10
array([10., 20., 30.])
>>> 
```
Notice that multiplying by 10 was carried out on each item in the array. 

More examples of array arithmetic: 

```
>>> banana * banana
array([1., 4., 9.])
>>> banana + banana
array([2., 4., 6.])
>>> banana2 = banana * 2
>>> print(banana2)
[2. 4. 6.]
>>> banana2 > banana
array([ True,  True,  True])
```

Evaluating arrays of different sizes is called *broadcasting* and will be discussed later. 


