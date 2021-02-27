# DataFrames, Continued. 

## Retrieving Values

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

When we created df5, the index was automatically assigned to be a numerical range. In some situations that may not be helpful or convenient. We have the ability to reassign the index column with df.set_index().

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
Want to name your index? We can do that too.

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

## Add a Row









