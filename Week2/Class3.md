# Reading and Importing Files Using Pandas

Now that you know how to work with smaller Series and DataFrames, we're going to switch gears a bit and learn to import larger files in formats you will encounter in the wild. These file types can contain a high volume of data. It will be good to learn using these types of files, to earn your own trust in your data manipulation abilities and practice real-life data analysis scenarios to assist in data science or business analysis. 

## Tabular Data

We may have mentioned Tabular Data before, but let's give it a proper definition:

Tabular data is data that is structured into rows/columns, like a table. Columns and rows are identified by headers/labels that explain the data located therein.  

## CSV Files

Need to import a CSV? Wait... what is a CSV? CSV is an acronym for Comma Separated Values, and may sometimes be referred to as Comma Delimited Files (Delimited is another way of saying Separated). A CSV is a plain text file that contains a list of data and are often used for exchanging data between different types of applications. For example, I can convert Microsoft Excel files (or even Google Spreadsheets) to CSV files and then import them as CSV into other applications. Considering how popular Excel is, knowing how to import CSV files is pretty handy. 

As expected, commas are used to delimit (separate) the data, but sometimes other characters, such as semicolons or spaces, can be used. 

![CSV](CSVimage.png)

Let's practice with a smaller file, first. In the folder Practice Files, you should find a file called "submission.csv". If you've downloaded these files into a folder, you'll need to check where are located so you provide the proper path to tell pandas where to look for the CSV file. 

We can import 'os' to check our operating system's current working directory to determine the path we need to supply to the file. In my case, I am working in SavvyDAPython, and the file is located within the PracticeFiles subfolder. 


```
>>> import os
>>> os.getcwd()
'/Users/melissapabst/SavvyPython/SavvyDAPython'
>>> df = pd.read_csv('PracticeFiles/submission.csv')
>>> df
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

It's a file with 1000 rows with two columns so larger than we are used to. When we first create the DataFrame it will give us a preview of the first and last rows, but we can use **.head()** to get a preview of the first five rows, specifically:

```
>>> df.head()
   Unnamed: 0  data
0           0     0
1           1     1
2           2     2
3           3     3
4           4     4
>>> 
```
