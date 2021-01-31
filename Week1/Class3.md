
# Vectorization, or Scalar Operations

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

# Universal Functions

Numpy has many universal mathematical functions as well, called **ufuncs**. These perform element-wise operations on ndarrays. 

They're fairly easy to apply, and once you get the hang of it they all work the same...

[Here is a list of current available Numpy ufuncs](https://numpy.org/doc/stable/reference/ufuncs.html#available-ufuncs)

Here we go!

```
>>> numeros = np.random.randint(10, size=10)
>>> numeros
array([3, 9, 7, 1, 8, 9, 6, 9, 5, 6])
>>> np.sum(numeros)
63
>>> np.sqrt(numeros)
array([1.73205081, 3.        , 2.64575131, 1.        , 2.82842712,
       3.        , 2.44948974, 3.        , 2.23606798, 2.44948974])
```

Here's a reciprocal function. Remember to examine your datatypes so you get the information returned you expect to get. 

```
>>> np.reciprocal(numeros)
array([0, 0, 0, 1, 0, 0, 0, 0, 0, 0])
>>> numeros.dtype
dtype('int64')
>>> numers = np.reciprocal(numeros.astype('float64'))
>>> numers
array([0.33333333, 0.11111111, 0.14285714, 1.        , 0.125     ,
       0.11111111, 0.16666667, 0.11111111, 0.2       , 0.16666667])
>>> 
```
As you can see, it is as easy as passing the array into the function to perform a mathematical operation:

```
>>> np.max(numeros)
9
>>> np.min(numeros)
1
>>> np.average(numeros)
6.3
```

Calculate a row or column sum:

```
>>> sully
array([[0, 0, 2],
       [0, 4, 0],
       [1, 4, 0]])
#all sum
>>> np.sum(sully)
11
#row sum
>>> np.sum(sully, axis = 1)
array([2, 4, 5])
#column sum
>>> np.sum(sully, axis = 0)
array([1, 8, 2])
#retain the 2D dimension of sully
>>> np.sum(sully, axis = 1, keepdims = True)
array([[2],
       [4],
       [5]])
```

Calculate a mean: 

```
>>> sully
array([[0, 0, 2],
       [0, 4, 0],
       [1, 4, 0]])
>>> sully.mean(axis = 0)
array([0.33333333, 2.66666667, 0.66666667])
>>> sully.mean(axis = 1)
array([0.66666667, 1.33333333, 1.66666667])
>>> 
```

# Reshaping and Transposing

Numpy ndarrays can be given a new shape without changing its data. Reshaping creates a new view object. 

```
>>> array = np.arange(45)
>>> array
array([ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11, 12, 13, 14, 15, 16,
       17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33,
       34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44])
>>> array.reshape(9, 5)
array([[ 0,  1,  2,  3,  4],
       [ 5,  6,  7,  8,  9],
       [10, 11, 12, 13, 14],
       [15, 16, 17, 18, 19],
       [20, 21, 22, 23, 24],
       [25, 26, 27, 28, 29],
       [30, 31, 32, 33, 34],
       [35, 36, 37, 38, 39],
       [40, 41, 42, 43, 44]])
>>> 
```

Remember, the first number in the tuple selects the matrix, so if we have a 1D array, the following is the same: 

```
>>> print(x)
[87 99 23  2 21 52  1 87 29 37]
>>> print(x.reshape(2, 5))
[[87 99 23  2 21]
 [52  1 87 29 37]]
>>> print(x.reshape(1, 2, 5))
[[[87 99 23  2 21]
  [52  1 87 29 37]]]
>>> 
```

Transposing uses the axis as a keyword argument. Let's flip some x's and y's to create a new view

Transposing a 1-D array returns an unchanged view of the original array.

```
>>> abc = np.arange(4).reshape((2, 2))
>>> abc
array([[0, 1],
       [2, 3]])
>>> np.transpose(abc)
array([[0, 2],
       [1, 3]])
>>> 
```
Transposing with more dimensions can be a real brain-teaser: 

2D: Three rows, two columns becomes two rows, three columns, or a 3x3 becomes another 3x3.

Note: We could use the array transpose method or the T attribute.

```
>>> baby = [[0,1], [2,3], [4,5]]
>>> baby = np.array(baby)
>>> baby
array([[0, 1],
       [2, 3],
       [4, 5]])
# Array transpose() function
>>> np.transpose(baby)
array([[0, 2, 4],
       [1, 3, 5]])]
# Note: baby keeps original shape & new array was created with transpose. You could store it in a varialbe if needed!
>>> baby
array([[0, 1],
       [2, 3],
       [4, 5]])
# T attribute
>>> baby.T
array([[0, 2, 4],
       [1, 3, 5]])
>>> 
       
```
3D: Transpose accepts a tuple of axis numbers. Remember we have three axes represented by (matrix, row, and column) as parameters. 

```
>>> myarray
array([[[ 0,  1,  2,  3],
        [ 4,  5,  6,  7],
        [ 8,  9, 10, 11]],

       [[12, 13, 14, 15],
        [16, 17, 18, 19],
        [20, 21, 22, 23]]])
>>> myarray.transpose((1, 0, 2))
array([[[ 0,  1,  2,  3],
        [12, 13, 14, 15]],

       [[ 4,  5,  6,  7],
        [16, 17, 18, 19]],

       [[ 8,  9, 10, 11],
        [20, 21, 22, 23]]])
>>> 
```
[This question in Stack Overflow resulted in an in-depth answer about how transpose() works. Read on if you want to learn about **strides**](https://stackoverflow.com/questions/32034237/how-does-numpys-transpose-method-permute-the-axes-of-an-array)



# Fancy Indexing

Fancy indexing is Numpy's way of indexing using integer arrays to create new arrays. 

Let's pass an array of indices to access multiple array elements at once: 

```
>>> x = rand.randint(100, size = 10)
>>> print(x)
[51 92 14 71 60 20 82 86 74 74]
# an okay but more laborious method
>>> [x[2], x[5], x[0], x[8]]
[14, 20, 51, 74]
# fancy indexing: pass an array of indices
>>> ind = [2, 5, 0, 8]
>>> print(x[ind])
[14 20 51 74]
>>> 
```
When we pass an ndarray as an index, the resulting shape is that of the index, not the original array. 

```
>>> print(x)
[51 92 14 71 60 20 82 86 74 74]
>>> ind2 = np.array([[2, 5], [0, 8]])
>>> print(x[ind2])
[[14 20]
 [51 74]]
>>> 
```
Passing ndarrays (2D and up) selects a 1D array of elements corresponding to tuples:

```
>>> y = np.arange(24).reshape(6, 4)
>>> print(y)
[[ 0  1  2  3]
 [ 4  5  6  7]
 [ 8  9 10 11]
 [12 13 14 15]
 [16 17 18 19]
 [20 21 22 23]]
>>> y[[1, 2, 3, 0], [0, 3, 2, 1]]
array([ 4, 11, 14,  1])
>>> 
```






Evaluating arrays of different sizes is called *broadcasting* and will be discussed later. 


