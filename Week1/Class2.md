# NumPy, continued.

## Warmup

We left off talking about the advantages of numpy ndarrays, and tonight we will delve into them further. But let's make sure you have the hang of creating a Numpy ndarray. 

Given the following, create a numpy array:

```
temps = [[[34.5, 65.3], [23.4, 65.0], [99.3, 96.3]],  [[23.4, 54.2], [32.4, 34.2], [12.4, 56.4]]]
```

Create numpy array.
What are its attributes? ndim? shape? size? dtype?

# Subsetting (Indexing) and Slicing

In our previous studies, we discussed **indexing**, or how to access subsets of data or elements of data within arrays. 

And remember, indexing begins with zero, so the location of the first item is [0], NOT [1].

One-dimensional arrays allow us to access innermost items with one set of '[ ]'. This selects an element in a row.

```
>>> banana = np.array([1, 2, 3])
>>> banana[1]
2
```

Two-dimensional arrays require two '[ ][ ]' to select the innermost element. This selects a [row] and a [column].

```
>>> a = np.array([[1, 2, 3],
...               [4, 5, 6],
...               [7, 8, 9]])
>>> a[0][1]
2
```

Using one [ ] with a two-dimensional array will return the first row.

```
>>> a[0]
array([1, 2, 3])
```


Three-dimensional arrays require three: '[ ][ ][ ]'. This selects a [matrix] a [row] and a [column].

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

What is the value at [1][2]?

What about [0][0][0]?

Keep practicing! 


Let's look at **slicing** ndarrays. When you use slicing techniques, you are creating a **view** of the original array. Slicing uses python's [start : stop : step] parameters structure, which you should already be familiar with.

Here is how we can work with a one-dimensional array:


```
>>> apples = np.arange(10)
>>> apples
array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])

# slice single item
>>> apples[2]
2

# slice items between indexes -- start at 5, stop at 8
>>> apples[5:8]
array([5, 6, 7])

# slice items starting from an index -- include all, starting at 2
>>> apples[2:]
[2  3  4  5  6  7  8  9]

# using negative indices selects items from the end:
>>> apples[-2]
8
```
A two-dimensional array adds complexity. First, examine the methods we used with one-dimensional arrays and apply them to two-dimensional arrays. The ellipsis syntax is used to indicate selecting in full any remaining unspecified dimensions.

```
>>> a = np.array([[1,2,3],[3,4,5],[4,5,6]]) 

# slice items starting from index 1
>>> a[1:]
array([[3, 4, 5],
       [4, 5, 6]])
       
# select first two rows of a
>>> a[:2]
array([[1, 2, 3],
       [3, 4, 5]])

# select first two rows, select columns starting at [1]
>>> a[:2, 1:]
array([[2, 3],
       [4, 5]])

# select first two rows, 3rd column
>>> a[:2, 2]
array([3, 5])

# using negative indices selects rows from the end
>>> a[:-2, 2]
array([3])

# return all items in second column
>>> a[...,1]
array([2, 4, 5])
>>> 
# return all items in second row
>>> a[1,...]
array([3, 4, 5])

# slice items from column one onwards
>>> a[...,1:]
array([[2, 3],
       [4, 5],
       [5, 6]])
```

You can find an explanation of indexing with top-notch visuals [here](https://www.pythoninformer.com/python-libraries/numpy/index-and-slice/#:~:text=Slicing%20an%20array,accessed%20in%20a%20different%20order.). Let's take a look at how they define axis, matrices, rows, and columns to solidify concepts. 

(Remember, axis 0 is rows, and axis 1 is columns)




# Copying arrays
We can use the np.copy function to store data
Consider this 3D array and how we can manipulate it:

```
>>> a3 = np.array([[[1, 2, 3], [4, 5, 6]], [[7, 8, 9], [10, 11, 12]]])
>>> a3[0]
array([[1, 2, 3],
       [4, 5, 6]])
>>> oldvalues = a3[0].copy
>>> a3[0]=47
>>> a3
array([[[47, 47, 47],
        [47, 47, 47]],

       [[ 7,  8,  9],
        [10, 11, 12]]])
```
>>> h = a.view() Create a view of the array with the same data
>>> np.copy(a) Create a copy of the array
>>> h = a.copy() Create a deep copy of the array


# Scalar Operations

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


