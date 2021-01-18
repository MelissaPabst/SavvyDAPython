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

In our previous studies, we discussed indexing, or how to access data within arrays. 

One-dimensional arrays allow us to access items with one set of '[]'

Two-dimensional arrays require two: '[][]'

Three-dimensional arrays require three: '[][][]'

What about four-dimensional arrays?

And remember, indexing begins with zero, so the location of the first item is [0].

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


# Mathematical Operations



