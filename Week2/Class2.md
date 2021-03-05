# DataFrames, Continued. 

## Retrieving Values: Indexing options 

Consider the following DataFrame: 

```
>>> data
{'student': ['Jane', 'Delilah', 'Kyle', 'Sam', 'Elaine', 'Arthur', 'Thomas'], 'grade': [97, 56, 76, 85, 99, 100, 98], 'age': [13, 13, 13, 13, 13, 14, 13]}
>>> df5 = pd.DataFrame(data)
>>> df5
   student  grade  age
0     Jane     97   13
1  Delilah     56   13
2     Kyle     76   13
3      Sam     85   13
4   Elaine     99   13
5   Arthur    100   14
6   Thomas     98   13
```

We briefly looked at .loc[] last class to retrieve a row. Let's expand its use and look at other methods. 

How do we get the name of the student at index 0? We have several options:


```
>>> df5.loc[0]['student'] 
'Jane'
>>> df5.iloc[0][0]
'Jane'
>>> df5.at[0, 'student']
'Jane'
>>> df5.iat[0, 0]
'Jane'
```
Note the subtle differences with each method:

.loc[] works on the labels of your index to access a group of rows/colums.

.iloc[] works on the integer positions in your index to access a group of rows/columns.

.at[] lets us access a single value for a row/column label pair.

.iat[] lest us access a single value for a row/column pair by integer position.


Let's do a quick practice and use the above methods to retrieve the following 2 values: 

1. Thomas's grade

2. Arthur's age

Get help if you need it!

We can use these methods with indexing & slicing!


```
>>> df5.iloc[3, [2]]
age    13
Name: 3, dtype: object
>>> df5.loc[3, ['grade']]
grade    85
Name: 3, dtype: object
>>> df5.loc[:3]
   student  grade  age
0     Jane     97   13
1  Delilah     56   13
2     Kyle     76   13
3      Sam     85   13
>>> df5.loc[df5.age > 12]
   student  grade  age
0     Jane     97   13
1  Delilah     56   13
2     Kyle     76   13
3      Sam     85   13
4   Elaine     99   13
5   Arthur    100   14
6   Thomas     98   13
>>> df5.iloc[:, :2][df5.age > 12]
   student  grade
0     Jane     97
1  Delilah     56
2     Kyle     76
3      Sam     85
4   Elaine     99
5   Arthur    100
6   Thomas     98
>>> df5.iloc[:, :1][df5.age > 12]
   student
0     Jane
1  Delilah
2     Kyle
3      Sam
4   Elaine
5   Arthur
6   Thomas
>>> 
```

We can also use Indexing and Slicing methods as we used with Python, NumPy, and panda Series:

```
>>> data = pd.DataFrame(np.arange(16).reshape((4,4),), index=['red', 'yellow', 'orange','green'], columns=['one', 'two', 'three', 'four'])
>>> data
        one  two  three  four
red       0    1      2     3
yellow    4    5      6     7
orange    8    9     10    11
green    12   13     14    15
>>> data['three']
red        2
yellow     6
orange    10
green     14
Name: three, dtype: int64
>>> data[['one', 'four']]
        one  four
red       0     3
yellow    4     7
orange    8    11
green    12    15
# provides row data
>>> data[:3]
        one  two  three  four
red       0    1      2     3
yellow    4    5      6     7
orange    8    9     10    11
# provides column data
>>> data['one']
red        0
yellow     4
orange     8
green     12
Name: one, dtype: int64
```

There is also the values attribute you can call on a df, which returns a 2D ndarray:

```
>>> df5.values
array([['Jane', 97, 13],
       ['Delilah', 56, 13],
       ['Kyle', 76, 13],
       ['Sam', 85, 13],
       ['Elaine', 99, 13],
       ['Arthur', 100, 14],
       ['Thomas', 98, 13]], dtype=object)
>>> 
```

## Retrieving Rows

What if we want all of the info on Jane? She is in row 0, so we can do the following:
 
```
>>> df5.iloc[0]
student    Jane
grade        97
age          13
Name: 0, dtype: object
>>> 
```

Try it yourself, but get the data for Elaine. 

## Retrieving Columns

Of course, if we wanted to do an average of the grades, we would need to gather all the grades, first. Let's do it!

```
>>> df5.loc[:,'grade']
0     97
1     56
2     76
3     85
4     99
5    100
6     98
Name: grade, dtype: int64
>>> 
```
Practice getting column data by getting the names of the students. 

## Set Your Own Index

When we created df5, the index was automatically assigned to be a numerical range spanning the size of your df. In some situations that may not be helpful or convenient. We have the ability to reassign the index column with df.set_index().

```
>>> df5
   student  grade  age
0     Jane     97   13
1  Delilah     56   13
2     Kyle     76   13
3      Sam     85   13
4   Elaine     99   13
5   Arthur    100   14
6   Thomas     98   13
>>> df5_new = df5.set_index('student')
>>> df5_new
         grade  age
student            
Jane        97   13
Delilah     56   13
Kyle        76   13
Sam         85   13
Elaine      99   13
Arthur     100   14
Thomas      98   13
>>>
```

Great news! Setting the index is reversible. Don't like it? Change it back with df.reset_index().

```
>>> df5_new
         grade  age
student            
Jane        97   13
Delilah     56   13
Kyle        76   13
Sam         85   13
Elaine      99   13
Arthur     100   14
Thomas      98   13
>>> df5_new.reset_index()
   student  grade  age
0     Jane     97   13
1  Delilah     56   13
2     Kyle     76   13
3      Sam     85   13
4   Elaine     99   13
5   Arthur    100   14
6   Thomas     98   13
>>> 
```
The method .reindex() allows us to create a new object with the data realigned to the new index: 

```
>>> df5
student info  student  height  grade  age
studentID                                
0                Jane      56     97   13
1             Delilah      62     56   13
2                Kyle      67     76   13
3                 Sam      54     85   13
4              Elaine      78     99   13
5              Arthur      76    100   14
6              Thomas      56     98   13
7               Steve      57     97   14
>>> df5_index = df5.reindex([1, 2, 3, 4, 5, 6, 7, 0])
>>> df5_index
student info  student  height  grade  age
studentID                                
1             Delilah      62     56   13
2                Kyle      67     76   13
3                 Sam      54     85   13
4              Elaine      78     99   13
5              Arthur      76    100   14
6              Thomas      56     98   13
7               Steve      57     97   14
0                Jane      56     97   13
>>> 
```
The columns can be reindexed with the columns keyword:


```
>>> df5_index = df5.reindex(columns = stats)
>>> df5_index
student info  student  grade  age  height
studentID                                
0                Jane     97   13      56
1             Delilah     56   13      62
2                Kyle     76   13      67
3                 Sam     85   13      54
4              Elaine     99   13      78
5              Arthur    100   14      76
6              Thomas     98   13      56
7               Steve     97   14      57
>>> 
```

Want to name your index? We can do that too, with the name attribute.

```
>>> df5
   student  grade  age
0     Jane     97   13
1  Delilah     56   13
2     Kyle     76   13
3      Sam     85   13
4   Elaine     99   13
5   Arthur    100   14
6   Thomas     98   13
>>> df5.index.name = 'studentID'
>>> df5
           student  grade  age
studentID                     
0             Jane     97   13
1          Delilah     56   13
2             Kyle     76   13
3              Sam     85   13
4           Elaine     99   13
5           Arthur    100   14
6           Thomas     98   13
>>> 
```
There is also a name attribute for columns:

```
>>> df5
           student  grade  age
studentID                     
0             Jane     97   13
1          Delilah     56   13
2             Kyle     76   13
3              Sam     85   13
4           Elaine     99   13
5           Arthur    100   14
6           Thomas     98   13
>>> df5.columns.name = 'student info'
>>> df5
student info  student  grade  age
studentID                        
0                Jane     97   13
1             Delilah     56   13
2                Kyle     76   13
3                 Sam     85   13
4              Elaine     99   13
5              Arthur    100   14
6              Thomas     98   13
>>> 
```

## Add a Row

We have a new student, Steve, who also took the test, so we need to add a row to our df. 

```
>>> df5.loc[7] = ['Steve', 97, 14]
>>> df5
student info  student  grade  age
studentID                        
0                Jane     97   13
1             Delilah     56   13
2                Kyle     76   13
3                 Sam     85   13
4              Elaine     99   13
5              Arthur    100   14
6              Thomas     98   13
7               Steve     97   14
>>> 
```

What do you think would happen if we assigned Steve to .loc[2] instead of .loc[7]?

```
>>> df5
student info  student  grade  age
studentID                        
0                Jane     97   13
1             Delilah     56   13
2                Kyle     76   13
3                 Sam     85   13
4              Elaine     99   13
5              Arthur    100   14
6              Thomas     98   13
7               Steve     97   14
>>> df5.loc[2] = ['Steve', 97, 14]
>>> df5
student info  student  grade  age
studentID                        
0                Jane     97   13
1             Delilah     56   13
2               Steve     97   14
3                 Sam     85   13
4              Elaine     99   13
5              Arthur    100   14
6              Thomas     98   13
7               Steve     97   14
>>> 
```
Dangit, we overwrote Kyle's info. We didn't want to do that! I hope we made a backup somewhere... 

There is also an append function to add a row, or an entire df: 

```
>>> df6 = pd.DataFrame({"grade":[87], "age":[13], "student":['Rex'], "height":[76]})
>>> df3
   grade  age  student height
0     97   13     Jane    NaN
1     56   13  Delilah    NaN
2     76   13     Kyle    NaN
3     85   13      Sam    NaN
4     99   13   Elaine    NaN
5    100   14   Arthur    NaN
6     98   13   Thomas    NaN
>>> df6
   grade  age student  height
0     87   13     Rex      76
>>> df3.append(df6)
   grade  age  student height
0     97   13     Jane    NaN
1     56   13  Delilah    NaN
2     76   13     Kyle    NaN
3     85   13      Sam    NaN
4     99   13   Elaine    NaN
5    100   14   Arthur    NaN
6     98   13   Thomas    NaN
0     87   13      Rex     76
>>> 
```
Pay attention to the index when using .append(). You can set "ingore_index" to True to avoid maintaining the index from the original df. In this case, pretend we needed the row to be assigned a new index number. 

```
>>> df3.append(df6, ignore_index=True)
   grade  age  student height
0     97   13     Jane    NaN
1     56   13  Delilah    NaN
2     76   13     Kyle    NaN
3     85   13      Sam    NaN
4     99   13   Elaine    NaN
5    100   14   Arthur    NaN
6     98   13   Thomas    NaN
7     87   13      Rex     76
>>> 
 ```
When we use .append(), columns not in the original df are added as new columns and the new cells are populated with NaN value. 

```
>>> df6 = pd.DataFrame({"grade":[87], "age":[13], "student":['Rex'], "height":[76], "hometown":["St. Louis"]})
>>> df3.append(df6)
   grade  age  student height   hometown
0     97   13     Jane    NaN        NaN
1     56   13  Delilah    NaN        NaN
2     76   13     Kyle    NaN        NaN
3     85   13      Sam    NaN        NaN
4     99   13   Elaine    NaN        NaN
5    100   14   Arthur    NaN        NaN
6     98   13   Thomas    NaN        NaN
0     87   13      Rex     76  St. Louis
>>> 
```
In a way, we just added a column! But let's look at more efficient ways to do that. 


## Add a column

We can append a column by adding a Series to an existing DataFrame using .loc[]:

```
>>> df5.loc[:,'height'] = pd.Series([56, 62, 67, 54, 78, 76, 56, 57])
>>> df5
student info  student  grade  age  height
studentID                                
0                Jane     97   13      56
1             Delilah     56   13      62
2                Kyle     76   13      67
3                 Sam     85   13      54
4              Elaine     99   13      78
5              Arthur    100   14      76
6              Thomas     98   13      56
7               Steve     97   14      57
>>> 
```
We can declare a list and convert it into a column:

```
>>> hometowns = ['Chicago', 'Minneapolis', 'Cairo', 'Vancouver', 'St. Louis', 'Seattle', 'Carbondale', 'Los Angeles']
>>> df5['birthplace'] = hometowns
>>> df5
student info  student  height  grade  age   birthplace
studentID                                             
0                Jane      56     97   13      Chicago
1             Delilah      62     56   13  Minneapolis
2                Kyle      67     76   13        Cairo
3                 Sam      54     85   13    Vancouver
4              Elaine      78     99   13    St. Louis
5              Arthur      76    100   14      Seattle
6              Thomas      56     98   13   Carbondale
7               Steve      57     97   14  Los Angeles
>>> 
```

We can use .assign() to return a new object with all original columns in addition to new ones:

```
>>> df5_towns = df5.assign(birthplace = hometowns)
>>> df5_towns
student info  student  height  grade  age   birthplace
studentID                                             
0                Jane      56     97   13      Chicago
1             Delilah      62     56   13  Minneapolis
2                Kyle      67     76   13        Cairo
3                 Sam      54     85   13    Vancouver
4              Elaine      78     99   13    St. Louis
5              Arthur      76    100   14      Seattle
6              Thomas      56     98   13   Carbondale
7               Steve      57     97   14  Los Angeles
>>> 
```

If appending (adding it to the end) is not what we want to do, we can instead use df.insert(), and place the column in a desired index. 

```
# insert(loc, column name, data, allow_duplicates)
>>> df5.insert(1, 'height', height, False)
>>> df5
student info  student  height  grade  age
studentID                                
0                Jane      56     97   13
1             Delilah      62     56   13
2                Kyle      67     76   13
3                 Sam      54     85   13
4              Elaine      78     99   13
5              Arthur      76    100   14
6              Thomas      56     98   13
7               Steve      57     97   14
>>> 
```
By far the easiest and most recommended method is to use .loc[], but as you have probably noticed there are multiple ways to accomplish the manipulation you need.


## Transpose

Swapping rows and columns is easy, and similar to transposing with NumPy arrays:

```
>>> df
        student  grade  age  height
red        Jane     97   13     NaN
orange  Delilah     56   13     NaN
yellow     Kyle     76   13     NaN
green       Sam     85   13     NaN
blue     Elaine     99   13     NaN
indigo   Arthur    100   14     NaN
violet   Thomas     98   13     NaN
>>> df.T
          red   orange yellow green    blue  indigo  violet
student  Jane  Delilah   Kyle   Sam  Elaine  Arthur  Thomas
grade      97       56     76    85      99     100      98
age        13       13     13    13      13      14      13
height    NaN      NaN    NaN   NaN     NaN     NaN     NaN
>>> 
```
 

