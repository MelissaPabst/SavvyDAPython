# Congratulations! 

You have reached the first night of the Data Analysis section of this class. Now that you have a grasp of the basics of the Python programming language (and if you don't, please reach out!), we can begin using that knowledge to leverage Python to work with large sets of data. 

Soon you will be well-prepared to take a set of data and turn it into a mind-blowing masterpiece of graphs and charts and communicate your findings. We'll be getting to the meat and potatoes of data analysis with Python a bit later, but first we need to discuss some basic fundamentals.

# Data Analysis Workflow

What are we going to learn in this section of the class? In what order? How do data scientists even approach their task? Well, over time an **iterative** process has been established. (Bonus: Can you tell me what 'iterative' means?) 

This process involves collecting data, preparing it, exploratory data analysis, and drawing conclusions. 

Let's look at what that process can look like: 

[Data Analysis Iteration with Roger Peng](https://www.youtube.com/watch?v=xOomNicqbkk)

Keep in mind, the process is heavily-based in data preparation and determining if the outcome of the step you took to wrangle the data meets expectations. 

1. Set expectations
2. Collect data/info
3. React to data and revise expectations if needed - What have we learned? What would we do differently next time? 

Repeat if necessary!

## Data Collection

There is no shortage of data in today's world. Shopping habits. Consumer info. Data from restaurant POS. Sports stats. Traffic studies. Population. Wall Street stocks. 

Data collection is a must-have first step as we cannot analyze data we do not have. But first we need to consider a few things:

1. What kind of data do we need? Data that is useful for our analysis. 
 
2. Where and how will we get the data?
    - Web scraping
    - APIs
    - Databases
    - Government websites
    - Financial resources
    - Log files

Remember we are looking for data relevant to our study. If we are looking for speeds of cars, do we need to know the cars' colors? No, but relevant data might be the terrain type or weather conditions or type of fuel used or weight of the car. The data you use will depend on the story you are trying to tell. 

## Data Wrangling

But what if the data we gather isn't perfect? No worries. There are processes used to get it into a workable format suitable for data analysis. Using these processes to clean data is called Data Wrangling. 

How can data be "dirty"???

	- Inconsistencies: STL instead of St. Louis or Saint Louis, or stl
	- Typos: What can a misplaced decimal point do?
	- Missing entries
	- Time/Date formats: military time, time zones, dd/mm/yy versus mm/dd/yyyy, etc.
	- Incomplete information: Think about optional questions in a survey. How would those have been recorded to your data set?
	- Proper scale or resolution: We need cups, not gallons so we will have to calculate corrections. 
	- Irrelevant fields: quantatative versus qualitativd, is it needed?
	- Format: We're looking for beeps, not boops, or maybe long to wide form
	- Data recording process was "messed up": maybe it was recorded in the wrong order and we're looking at a descending timeline instead of an ascending one

Brain exercise: What are some data quality issues that cannot be fixed?





