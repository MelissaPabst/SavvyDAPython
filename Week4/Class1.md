# Date/Time Manipulation

![DarkestTimeline](week4images/darkesttimeline.jpeg)


Congrats! You're a pizza delivery driver! You've loaded all the delivery data for one year into a csv and have only ten complaints on the following dates. You hope to use this data to show improvement and how you've decreased complaints over last year. You're thinking that with some good data in-hand you can prove your case. But silly you [and your team]... you weren't great at recording dates in a uniform fashion:

```
>>> dates = pd.read_csv('PracticeFiles/datesandtimes.csv')
>>> dates
   value  pizzas                      date/time
0      0       2                  11/6/2021 1PM
1     10       5       Thursday March 12th 10am
2     20       1                       12/22/21
3     30       2                     10/12/2021
4     40       3               12-11-2021 00:00
5     50       8                      30/1/2021
6     60       1                         FRIDAY
7     70      12                     2021-03-01
8     80      13                     2021/03/01
9     90       1  2021-03-22 15:16:45.433000088
```

There's nothing I can help you with the poor recording methods, but maybe after we go over some Date and Time tools you can fix your data yourself and maybe learn to record better. 

First let's talk about time a little bit:

Time zones: The best time zone to use (and probably most standard) is UTC, or Coordinated Universal Time (Greenwich Mean Time), which doesn't use Daylight Savings Time. For example, this ‘2021-07-01 13:00:00−04:00’ is in ISO 8601, and in English it means “July 1st, 2000 @ 1PM, 4 hours behind UTC”. But it might not always be perfect because the -05:00 or whatever timezone you are referring to may or not be using Daylight Savings time. 

Military time: If you don't understand military time, [here is a primer](https://militarybase.net/military-time-converter/). Fun fact: You might also see ‘2021-07-01 13:00:00−00:00’ as '2021-07-01 13:00:00−Z', with the '-Z' denoting it is talking about UTC. The 'Z' comes from [military time zone names](https://www.worldtimezone.com/wtz-map-military.html) and is short for "zulu".  

Timestamps: Specific instances in time, or when a certain event occurred. Examples are 'time of death' or a date/time on a red light camera. They are sometimes accurate to fractions of seconds. 

Periods: These are fixed lengths of time, such as March 2021, or the year 2021. Or the 00:00 hour. 

Intervals: Intervals are a period of time indicated by a start and end timestamp. (Periods are mores general, and intervals can be constructed by timestamps of your own choosing.)

Elapsed time: These usually have to do with experimentation; the time period over xyz was supposed to demonstrate a result. 


### Python Datetime

Python **[datetime](https://docs.python.org/3/library/datetime.html)** is a good place to start. 

```
>>> from datetime import datetime
# I'll import datetime as dt so it's less tedious to type
>>> from datetime import datetime as dt
>>> from datetime import date
```

We can make dates, but datetimes are more specific:

```
>>> my_date = date(2021, 4, 14)
# year, month, day
>>> my_date
datetime.date(2021, 4, 14)
>>> my_datetime = datetime(2021, 4, 14)
# year, month, day, hour, minute, second, microsecond
>>> my_datetime
datetime.datetime(2021, 4, 14, 0, 0)
>>> 
```

What does 'now' look like?

```
>>> now = dt.now()
>>> now
# year, month, day, hour, minute, second, microsecond
datetime.datetime(2021, 4, 16, 17, 25, 39, 208270)
>>> now.year
2021
>>> now.month
4
>>> now.day
16
>>> now.second
39
>>> now.year, now.month, now.day
(2021, 4, 16)
```

We can calculate differences on datetime objects to determine timeframes. 

``` 
# less than one day
>>> delta = dt(2021, 4, 12) - dt(2021, 4, 11, 3, 2, 1)
>>> delta
datetime.timedelta(seconds=75479)
# more than one day
>>> delta2 = dt(2021, 4, 12) - dt(2021, 4, 10, 3, 2, 1)
>>> delta2
datetime.timedelta(days=1, seconds=75479)
>>> 
```

We use **timedelta** to shift a timedate object by a desired increment:

```
>>> from datetime import timedelta as td
>>> start = dt(2021, 4, 12)
>>> start + td(1)
datetime.datetime(2021, 4, 13, 0, 0)
>>> start - td(1)
datetime.datetime(2021, 4, 11, 0, 0)
>>> start + td(1)*2
datetime.datetime(2021, 4, 14, 0, 0)
```

Often we will have a datetime and want it in another format:

```
>>> timestamp = dt(2021, 4, 13)
>>> timestamp
datetime.datetime(2021, 4, 13, 0, 0)
# note the difference as a string and not a datetime object:
>>> str(timestamp)
'2021-04-13 00:00:00'
```

Let's take a moment to learn about Python's datetime formatting codes:

Go [here](https://strftime.org/) and poke around. We'll be using these codes to reformat datetime objects and strings.

What is the difference between '%y' and '%Y'?


We can use the **strftime()** method to format our datetime object to a string:

```
>>> timestamp.strftime('%m/%d/%Y')
'04/13/2021'
>>> 
```

And **strptime()** formats a string to a datetime object. 

```
>>> dt_string = timestamp.strftime('%m-%d/%y')
>>> dt_string
'04-13/21'
# we have to tell it the exact format the date appears as in the string, if you know the format. Here we're telling it there's a month, followed by a dash, followed by a day, and then there's a slash, and there is a two-digit year.
>>> timestamp2 = dt.strptime(dt_string, '%m-%d/%y')
>>> timestamp2
datetime.datetime(2021, 4, 13, 0, 0)
>>> 
```

Another way to format a string to a datetime object is with **parse**. Parse is fairly good at predicting what is meant by different date formats:

```
>>> from dateutil.parser import parse
>>> parse('July 15, 2021')
datetime.datetime(2021, 7, 15, 0, 0)
>>> 
```

Parse is also helpful with international dates, where the day comes first (Christmas would be 25/12/2021 instead of 12/25/2021). If you pass in dayfirst=True you can rearrange those pesky backwards dates. This took a bit of time for me to figure out, but if you pass the first number over 12, it will automatically reverse the day/month to month/day. Otherwise you have to specify you want the day first: 

```
>>> parse("25-12-21")
datetime.datetime(2021, 12, 25, 0, 0)
>>> parse("13-12-21")
datetime.datetime(2021, 12, 13, 0, 0)
>>> parse("10-12-21")
datetime.datetime(2021, 10, 12, 0, 0)
>>> parse("10-12-21", dayfirst=True)
datetime.datetime(2021, 12, 10, 0, 0)
>>> 
```

### NumPy Datetime

[Here is the documentation](https://numpy.org/doc/stable/reference/arrays.datetime.html) for NumPy datetime functions. 

Creating a NumPy datetime object is pretty straightforward:

```
>>> npdt = np.datetime64('2021-04-20')
>>> npdt
numpy.datetime64('2021-04-20')
>>> 
```

Note: The '64' comes from int64. NumPy couldn't use 'datetime' because it was already a library in Python, so hence 'datetime64'. 

We can force a 'day' unit with passing 'D':

```
>>> npdt = np.datetime64('2021-04', 'D')
>>> npdt
numpy.datetime64('2021-04-01')
```

And, like NaN, we have 'NaT' for 'Not a time':

```
>>> np.datetime64('nat')
numpy.datetime64('NaT')
>>> 
```

When creating NumPy arrays of dates, we can specify the dtype=datetime64:

```
>>> npdts = np.array(['2022-03-03', 'NaT', '2021-04-21'], dtype='datetime64')
>>> npdts
array(['2022-03-03',        'NaT', '2021-04-21'], dtype='datetime64[D]')
>>> npdts = np.array(['2022-03-03', 'NaT', '2021-04-21'], dtype='datetime64[ms]')
>>> npdts
array(['2022-03-03T00:00:00.000',                     'NaT',
       '2021-04-21T00:00:00.000'], dtype='datetime64[ms]')
>>> 
```
Because we specified 'datetime64[ms]', if we add to it, it gets added as a millisecond:

```
>>> npdts
array(['2022-03-03T00:00:00.000',                     'NaT',
       '2021-04-21T00:00:00.000'], dtype='datetime64[ms]')
>>> npdts + 1
array(['2022-03-03T00:00:00.001',                     'NaT',
       '2021-04-21T00:00:00.001'], dtype='datetime64[ms]')
>>> 
```


If we add one to this array of datatimes, we get one month ahead:

```
>>> npdt = np.datetime64('2021-04')
>>> npdt + 1
numpy.datetime64('2021-05')
```

If we add one here, we get one day ahead: 

```
>>> npdt = np.datetime64('2021-04-01')
>>> npdt + 1
numpy.datetime64('2021-04-02')
>>> 
```

We can specify where we want the increment to appear. Here, it added a second:

```
>>> npdt = np.datetime64('2021-04', 's')
>>> npdt + 1
numpy.datetime64('2021-04-01T00:00:01')
```

### Pandas Timestamp


[Dates and Times in Pandas](https://pandas.pydata.org/pandas-docs/stable/user_guide/timeseries.html)

Creating a datetime object in Pandas is pretty easy. Actually, the Timestamp class is a wrapper class for NumPy's datetime64.:

```
>>> stamp = pd.to_datetime('2021-2-6')
>>> stamp
Timestamp('2021-02-06 00:00:00')
```
We can add a timezone with **tz_localize()** ([List of timezones here](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)):

```
>>> stamp = pd.to_datetime('2021-2-6').tz_localize('America/Chicago')
>>> stamp
Timestamp('2021-02-06 00:00:00-0600', tz='America/Chicago')
```
We can format our Timestamp by telling pandas how to read our string:

```
>>> stamp = pd.to_datetime('February 6, 2021', format='%B %d, %Y').tz_localize('America/Chicago')
>>> stamp
Timestamp('2021-02-06 00:00:00-0600', tz='America/Chicago')
```

We can call the time zone information with **.tz**.

```
>>> stamp.tz
<DstTzInfo 'America/Chicago' CST-1 day, 18:00:00 STD>
```

We can change time zones with **tz_convert()**: 

```
>>> stamp_africa = stamp.tz_convert('Africa/Abidjan')
>>> stamp_africa
Timestamp('2021-02-06 06:00:00+0000', tz='Africa/Abidjan')
>>> 
```
Suppose we have a list of dates:

```
>>> dates = np.array(['2011-01-01', pd.NA, '2021-07-04'])
```
We can pass it into **to_datetime** to return a DatetimeIndex. This object could be used as the index of a Series or DataFrame!:

```
>>> dates_stamp = pd.to_datetime(dates)
>>> dates_stamp
DatetimeIndex(['2011-01-01', 'NaT', '2021-07-04'], dtype='datetime64[ns]', freq=None)
>>>
```

Cool! That pd.NA converted to 'NaT'. 

Let's pass the DatetimeIndex into a Series:

```
>>> dates_series = pd.Series(dates_stamp)
>>> dates_series
0   2011-01-01
1          NaT
2   2021-07-04
dtype: datetime64[ns]
>>> 
```
Scalar values from DatetimeIndex are pandas Timestamp objects:

```
>>> dates_series[0]
Timestamp('2011-01-01 00:00:00')
>>> 
```

Anywhere you would use a datetime object, you can substitute a pandas Timestamp. Time series behaves like any other Series when indexing and selecting, and you can use datetime objects to slice. You can do range queries as well:

```
>>> long = pd.Series(np.random.randn(15), index=pd.date_range('1/1/2020', periods=15))
>>> long
2020-01-01   -1.063463
2020-01-02   -0.546160
2020-01-03    0.695083
2020-01-04    0.132825
2020-01-05    0.295902
2020-01-06   -1.612766
2020-01-07    0.882752
2020-01-08   -0.159633
2020-01-09    0.470423
2020-01-10   -1.438588
2020-01-11    1.730698
2020-01-12    0.813828
2020-01-13    0.064049
2020-01-14    0.184008
2020-01-15   -0.749361
Freq: D, dtype: float64
>>> 
```

Range query:

```
>>> long['1/5/2020':'1/12/2020']
2020-01-05    0.295902
2020-01-06   -1.612766
2020-01-07    0.882752
2020-01-08   -0.159633
2020-01-09    0.470423
2020-01-10   -1.438588
2020-01-11    1.730698
2020-01-12    0.813828
Freq: D, dtype: float64
>>> 
```

Query by year or month (returns all results, in this case):

```
>>> long['2020']
2020-01-01   -1.063463
2020-01-02   -0.546160
2020-01-03    0.695083
2020-01-04    0.132825
2020-01-05    0.295902
2020-01-06   -1.612766
2020-01-07    0.882752
2020-01-08   -0.159633
2020-01-09    0.470423
2020-01-10   -1.438588
2020-01-11    1.730698
2020-01-12    0.813828
2020-01-13    0.064049
2020-01-14    0.184008
2020-01-15   -0.749361
Freq: D, dtype: float64
>>> long['2020-01']
2020-01-01   -1.063463
2020-01-02   -0.546160
2020-01-03    0.695083
2020-01-04    0.132825
2020-01-05    0.295902
2020-01-06   -1.612766
2020-01-07    0.882752
2020-01-08   -0.159633
2020-01-09    0.470423
2020-01-10   -1.438588
2020-01-11    1.730698
2020-01-12    0.813828
2020-01-13    0.064049
2020-01-14    0.184008
2020-01-15   -0.749361
Freq: D, dtype: float64
>>> 
```

And it's not too picky about the format passed in. You can pass in a string date, datetime, for timestamp:

```
>>> long['01-2020']
2020-01-01   -1.063463
2020-01-02   -0.546160
2020-01-03    0.695083
2020-01-04    0.132825
2020-01-05    0.295902
2020-01-06   -1.612766
2020-01-07    0.882752
2020-01-08   -0.159633
2020-01-09    0.470423
2020-01-10   -1.438588
2020-01-11    1.730698
2020-01-12    0.813828
2020-01-13    0.064049
2020-01-14    0.184008
2020-01-15   -0.749361
Freq: D, dtype: float64
>>> 
```

Suppose we had a Series that had multiple observations (rows!) on the same timestamp, and we create a Series:

```
>>> days = pd.DatetimeIndex(['2/14/2021', '7/4/2021', '5/9/2021', '7/4/2021', '7/4/2021'])
>>> days_ts = pd.Series(np.arange(5), index=days)
>>> days_ts
2021-02-14    0
2021-07-04    1
2021-05-09    2
2021-07-04    3
2021-07-04    4
dtype: int64
>>>
```

We can confirm the index is not unique:

```
>>> days_ts.index.is_unique
False
>>>
```

The source of our duplications:

```
>>> days_ts['7/4/2021']
2021-07-04    1
2021-07-04    3
2021-07-04    4
dtype: int64
```

And then we can aggregate the data having non-unique timestamps. We can use groupby() and pass in level=0, and perform whatever data operation we need:

```
>>> grouped = days_ts.groupby(level=0)
>>> grouped.count()
2021-02-14    1
2021-05-09    1
2021-07-04    3
dtype: int64
>>> grouped.mean()
2021-02-14    0.000000
2021-05-09    2.000000
2021-07-04    2.666667
dtype: float64
>>> 
```
If we want to add/subtract time, we use a Timedelta. Let's add 6 hours to our times_series, by passing a value=6, and unit='H' for hours:

```
>>> dates_series
0   2011-01-01
1          NaT
2   2021-07-04
dtype: datetime64[ns]
>>> dates_series + pd.Timedelta(value=6, unit='H')
0   2011-01-01 06:00:00
1                   NaT
2   2021-07-04 06:00:00
dtype: datetime64[ns]
>>> 
```

Reminder: Delta means "change", and in our case we're talking about change in time. What kind of object would be returned if we subract two timestamps?

Hint: try pd.to\_datetime('a date') - pd.to\_datetime('another date')



















