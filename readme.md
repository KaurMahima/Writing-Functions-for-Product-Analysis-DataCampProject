# BIS 634 01 (FA22): Computational Methods for Informatics

## *Assignment 1*

### *Submitted By : Mahima Kaur*

------------------------------------------------------------------------

### Exercise 1

#### Write a function temp_tester that takes a definition of normal body temperature and returns a function that returns True if its argument is within 1 degree of normal temperature (i.e. the value is a healthy temperature), and False if not.

#### *Below is the response for Exercise 1:*

#### The code is the function that takes a definition of normal body temperature and returns a function that returns True if its argument is within 1 degree of normal temperature and False if not.

``` python

def temp_tester(temp):

  def inner_function(x):
    if x <= temp + 1 and x >= temp -1:
      return True
    else:
      return False
     
  return inner_function
```

#### Assigning the normal temperature values of human and chickens to the function.

``` python
human_tester = temp_tester(37) 
chicken_tester = temp_tester(41.1)
```

#### Testing the function developed.

``` python
print(chicken_tester(42))
print(human_tester(42))
print(chicken_tester(43))
print(human_tester(35))  
print(human_tester(98.6))
```

------------------------------------------------------------------------

### Excerise 2

#### Download the sqlite3 database from hw1-population.db.

#### Importing the dataset

``` python
import pandas as pd
import sqlite3
with sqlite3.connect("/Users/mahimakaur/Downloads/hw1-population.db") as db:
    data = pd.read_sql_query("SELECT * FROM population", db)
```

#### Exercise 2: Part 1 : Examine data. What columns does it have? How many rows does it have?

#### Response : The dataset has four columns namely : *name*, *age*, *weight*, *eyecolor*. There are *152361* rows (people) in the dataset.

*Below is the code to find the columns and number of rows in the dataset.*

``` python

data.info()

print("The columns in the data include:", ", ".join(list(data.columns)))
print("There are", data['name'].count(), "rows in the data")
```

#### Exercise 2: Part 2 : Examine the distribution of the ages in the dataset. In particular, be sure to have your code report the mean, standard deviation, minimum, maximum. Plot a histogram of the distribution with an appropriate number of bins for the size of the dataset (describe in your readme the role of the number of bins). Comment on any outliers or patterns you notice in the distribution of ages.

#### Response: The mean age is 39.5 years, and the maximum age included in the dataset is 99 years. It is important to have appropriate number of bins as if we take less bins, the histogram doesn't portray the data accurately. If large number of bins are used, the graph does not give a sense of the distribution of the dataset.

#### *Below is the code to examine the distribution of ages in the dataset.*

``` python
data['age'].describe() 
```

#### *Below is the code used to plot the histogram for the variable age.*

``` python
## Importing Libraries

import matplotlib.pyplot as plt
import numpy as np

age = data['age'] #Creating a variable age

## Calculating bins for the histogram 

q25, q75 = np.percentile(age, [25, 75])
bin_width = 2 * (q75 - q25) * len(age) ** (-1/3)
bins = round((age.max() - age.min()) / bin_width)
print("Freedman–Diaconis number of bins:", bins)

## Histogram Plot

plt.hist(age, bins=bins);
plt.ylabel('Count')
plt.xlabel('Age')
plt.title('Age Distribution of the Population')
```

![](download.png)
