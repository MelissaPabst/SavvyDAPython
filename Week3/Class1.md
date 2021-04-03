# Data, data, and more data

We ended last week with knowing **how** to import data, but there are things we didn't tell you... 

![DataMeme](week3images/datameme.jpeg)

Let's revisit CSV files, since those are probably what you will use most. 

CSV files (and other file types!) can require extra effort to get them to appear how you want. 

Recall "bunchofnumbers.csv"? Once we made the dataframe, it didn't have a title, and wasn't labeled very well. It has an "Unnamed" header row we don't want... Eh, I don't like it. 

```
>>> results = pd.read_csv('practicefiles/bunchofnumbers.csv')
>>> print(results)
     Unnamed: 0  data
0             0     0
1             1     1
2             2     2
3             3     3
4             4     4
..          ...   ...
995         995   995
996         996   996
997         997   997
998         998   998
999         999   999

[1000 rows x 2 columns]
```

There are many parameters ([close to 50 for CSV files, alone!](https://pandas.pydata.org/docs/reference/api/pandas.read_csv.html)) we can use to remedy data issues we encounter.

 Let's remove the header: 
 
 ```
>>> results = pd.read_csv('practicefiles/bunchofnumbers.csv', header=None)
>>> print(results)
          0     1
0       NaN  data
1       0.0     0
2       1.0     1
3       2.0     2
4       3.0     3
...     ...   ...
996   995.0   995
997   996.0   996
998   997.0   997
999   998.0   998
1000  999.0   999

[1001 rows x 2 columns]
```

What happened? That may have been a dumb move, but everything is fixable! Let's name the columns what we actually want them to be:  

```
>>> results = pd.read_csv('practicefiles/bunchofnumbers.csv', names=['apples', 'bananas'])
>>> print(results.head(5))
   apples bananas
0     NaN    data
1     0.0       0
2     1.0       1
3     2.0       2
4     3.0       3
>>> 
```

Back to our "mistake"... When we named the header=None, it took the existing header and made it the data for the first row. Does anyone remember how to remove a row?

```
>>> results.drop(0).head(5)
   apples bananas
1     0.0       0
2     1.0       1
3     2.0       2
4     3.0       3
5     4.0       4
>>> 
```

Did we just create a view or a copy? Here's a hint:

```
>>> results2 = results.drop(0).head(5)
>>> results2
   apples bananas
1     0.0       0
2     1.0       1
3     2.0       2
4     3.0       3
5     4.0       4
>>> 
```
If we were to convert "scary_pets_2" into a dataframe:

```
>>> results = pd.read_csv('practicefiles/scary_pets2.csv')
>>> print(results.head(5))
   id  location animal
0   0  1.098952   lion
1   1 -1.112979   lion
2   2  0.228454   lion
3   3  0.299128   lion
4   4  0.181097  tiger
```

But maybe we want it to be indexed by location:

```
>>> results = pd.read_csv('practicefiles/scary_pets2.csv', index_col='location')
>>> print(results.head(5))
           id animal
location            
 1.098952   0   lion
-1.112979   1   lion
 0.228454   2   lion
 0.299128   3   lion
 0.181097   4  tiger
>>> 
```
Open 'yucky.csv' and have a gander. 

![yucky](week3images/yuckycsvimage.jpg)

Consider the outcome of turning "yucky" into a dataframe: 


```
>>> results = pd.read_csv('practicefiles/yucky.csv')
>>> print(results)
                                             I'm a jerk
may                                june july     august
0                                  0    0             0
1                                  1    14           13
2                                  2    22           32
3                                  3    5            67
I put this here                    NaN  NaN         NaN
4                                  4    65           34
5                                  5    61           12
6                                  6    45           32
7                                  7    90           11
To make your life difficult        NaN  NaN         NaN
8                                  8    34           23
9                                  9    23           33
What are you going to do about it? NaN  NaN         NaN
10                                 10   11           11
>>> 
```

What can we do to prevent that gunk from clogging up our works? I mean, we don't want NaN,  nor rows that provide no value, right? 

```
>>> results2 = pd.read_csv('practicefiles/yucky.csv', skiprows=[0, 6, 11, 14])
>>> print(results2)
    may  june  july  august
0     0     0     0       0
1     1     1    14      13
2     2     2    22      32
3     3     3     5      67
4     4     4    65      34
5     5     5    61      12
6     6     6    45      32
7     7     7    90      11
8     8     8    34      23
9     9     9    23      33
10   10    10    11      11
>>> 
```
So clean!

A good practice is to examine our data before converting it so we can prevent yucky stuff from ending up in our dataframe. There are ways to fix it once the dataframe was created, but there are a multitude of parameters to consider before even converting to a dataframe.

## Inspecting a DataFrame Object

I snagged a larger CSV file from [SpatialKey](https://support.spatialkey.com/spatialkey-sample-csv-data/) that contains data from Sacremento real estate transactions. 

I want to put this in a dataframe so I can gather information about the data:

```
>>> real = pd.read_csv('practicefiles/sacremento.csv')
```
And then once I have it in a dataframe, I can get properties of the dataframe and the data within it:

```
>>> real.empty
False
>>> real.shape
(985, 12)
```

My dataframe is definitely not empty and has 985 rows/observations with 12 columns/variables. What are the columns? 

```
>>> real.columns
Index(['street', 'city', 'zip', 'state', 'beds', 'baths', 'sq__ft', 'type',
       'sale_date', 'price', 'latitude', 'longitude'],
      dtype='object')
```
   
Great! Those are definitely data types I would expect to find in a real estate CSV. 

Let's get a closer look at the data: 

```
>>> real.head()
             street        city    zip state  beds  ...         type                     sale_date  price   latitude   longitude
0      3526 HIGH ST  SACRAMENTO  95838    CA     2  ...  Residential  Wed May 21 00:00:00 EDT 2008  59222  38.631913 -121.434879
1       51 OMAHA CT  SACRAMENTO  95823    CA     3  ...  Residential  Wed May 21 00:00:00 EDT 2008  68212  38.478902 -121.431028
2    2796 BRANCH ST  SACRAMENTO  95815    CA     2  ...  Residential  Wed May 21 00:00:00 EDT 2008  68880  38.618305 -121.443839
3  2805 JANETTE WAY  SACRAMENTO  95815    CA     2  ...  Residential  Wed May 21 00:00:00 EDT 2008  69307  38.616835 -121.439146
4   6001 MCMAHON DR  SACRAMENTO  95824    CA     2  ...  Residential  Wed May 21 00:00:00 EDT 2008  81900  38.519470 -121.435768

[5 rows x 12 columns]
```

And the last several rows:

```
>>> real.tail()
                  street             city    zip state  ...                     sale_date   price   latitude   longitude
980   9169 GARLINGTON CT       SACRAMENTO  95829    CA  ...  Thu May 15 00:00:00 EDT 2008  232425  38.457679 -121.359620
981      6932 RUSKUT WAY       SACRAMENTO  95823    CA  ...  Thu May 15 00:00:00 EDT 2008  234000  38.499893 -121.458890
982    7933 DAFFODIL WAY   CITRUS HEIGHTS  95610    CA  ...  Thu May 15 00:00:00 EDT 2008  235000  38.708824 -121.256803
983     8304 RED FOX WAY        ELK GROVE  95758    CA  ...  Thu May 15 00:00:00 EDT 2008  235301  38.417000 -121.397424
984  3882 YELLOWSTONE LN  EL DORADO HILLS  95762    CA  ...  Thu May 15 00:00:00 EDT 2008  235738  38.655245 -121.075915

[5 rows x 12 columns]
```

So far, so good. But let's get more info about the column data types with **.dtypes**. 

```
>>> real.dtypes
street        object
city          object
zip            int64
state         object
beds           int64
baths          int64
sq__ft         int64
type          object
sale_date     object
price          int64
latitude     float64
longitude    float64
dtype: object
```

And using **info()**, we are provided with a nice summarization of the dataframe:

```
>>> real.info()
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 985 entries, 0 to 984
Data columns (total 12 columns):
 #   Column     Non-Null Count  Dtype  
---  ------     --------------  -----  
 0   street     985 non-null    object 
 1   city       985 non-null    object 
 2   zip        985 non-null    int64  
 3   state      985 non-null    object 
 4   beds       985 non-null    int64  
 5   baths      985 non-null    int64  
 6   sq__ft     985 non-null    int64  
 7   type       985 non-null    object 
 8   sale_date  985 non-null    object 
 9   price      985 non-null    int64  
 10  latitude   985 non-null    float64
 11  longitude  985 non-null    float64
dtypes: float64(2), int64(5), object(5)
memory usage: 92.5+ KB
```

The **.info()** method does a great job of providing us a way to see how many non-null entries in each column we have. In the above example we have none; all 985 values in all 12 columns are accounted for. 

Remember: Null values are missing values, and in pandas are represented by **None** for objects and **NaN** for non-numeric values in a float or integer column. 

So now we know a bit more about our real estate dataframe, we can begin to try to make sense of the data. 

## Describing Data / Summary Statistics

So far, we have a good idea about the properties of our dataframe, but we don't know much about our actual data and what it can tell us. Our next step is to get summary statistics with the **.describe()** method:

```
>>> real.describe()
                zip        beds       baths       sq__ft          price    latitude   longitude
count    985.000000  985.000000  985.000000   985.000000     985.000000  985.000000  985.000000
mean   95750.697462    2.911675    1.776650  1314.916751  234144.263959   38.607732 -121.355982
std       85.176072    1.307932    0.895371   853.048243  138365.839085    0.145433    0.138278
min    95603.000000    0.000000    0.000000     0.000000    1551.000000   38.241514 -121.551704
25%    95660.000000    2.000000    1.000000   952.000000  145000.000000   38.482717 -121.446127
50%    95762.000000    3.000000    2.000000  1304.000000  213750.000000   38.626582 -121.376220
75%    95828.000000    4.000000    2.000000  1718.000000  300000.000000   38.695589 -121.295778
max    95864.000000    8.000000    5.000000  5822.000000  884790.000000   39.020808 -120.597599
>>> 
```
Using **.describe()** returned a 5-number summary along with count, mean, and standard deviation for the seven columns with numeric data types (int64 or float64, in this case).   

Let's examine those values and their meanings:

**count**: This is the total number of data points in the column used to calculate other stats. 

**mean**: This is the average. All data point is added up and divided by the total number of data points. See [here](https://www.mathsisfun.com/mean.html#:~:text=How%20to%20Find%20the%20Mean,sum%20divided%20by%20the%20count.) for more on how to compute mean/averages.  

**std**: Standard deviation. It's a measure of how spread out numbers are. You can read about standard deviation [here](https://www.mathsisfun.com/data/standard-deviation.html). 

**5-number summary**: This is a statistics grouping that includes the minimum value, the 25% quadrant, the median (50%, or middle value), the 75% quadrant, and the maximum value. More about the 5-number summary can be found [here](https://www.thoughtco.com/what-is-the-five-number-summary-3126237).

(Note: You will have some of these computations as homework. It's important to know the meaning behind the numbers you deliver to a customer and be able to explain how you arrived at those values. This is a data analysis class--of course it involves math! It's nice that we have pandas to do the math for us, but you still need to understand the concepts.)