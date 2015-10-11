---
layout: post
title:  "Pandas Short Tutorial - Pandas is like R"
date:   1999-01-01 00:00:00
categories: python2r
---


- Pandas makes python like R, which enables a lot of basic operations that R can do.
- This tutorial is based on python 3.4 and pandas 0.16.2
- Also take a look at the other post: <a href="http://shengqiu.github.io/python2r/1999/01/01/use-python-as-r.html">Pandas is like R</a>
	
--- 

## Even before dataframe

#### Firstly we can check out the pandas series

The pandas series is pretty awesome, we can have an index, and you can call both `s[['A','C']]`  and s[0:2]. So essentially, this is a dictionary and a list at the same time.

{% highlight python%} 
s = pd.Series([7, 'Heisenberg', 3.14, -1789710578, 'Happy Eating!'],index=['A', 'Z', 'C', 'Y', 'E'])
{% endhighlight %}

or you can do this:

{% highlight python%} 
s_dict = {'A':7,'Z': 'Heisenberg','C': 3.14, 'Y':-1789710578, 'E':'Happy Eating!'}
s = pd.Series(s_dict)
{% endhighlight %}

Then we have our favarite R syntax:

{% highlight python%} 
s == 7
s[s==7]
{% endhighlight %}

- `s[s>1]` return any string
- `s[s<1]` does return any string
- `s[type(s) is int]` won't do what you want... have to do this:`s[[type(ss) is int for ss in s]`

---

## Read and Write dataframe

#### Load data frame from csv

The chunksize parameter defines how many lines in total

{% highlight python%} 
import pandas as pd
df = pd.read_csv('test.csv', chunksize=10000)
{% endhighlight %}

Another really cool example using the lambda function

{% highlight python%} 
headers = ['name', 'title', 'department', 'salary']
chicago = pd.read_csv('city-of-chicago-salaries.csv',header=False,names=headers,converters={'salary': lambda x: float(x.replace('$', ''))})
{% endhighlight %}

Here `lambda x: float(x.replace('$',''))` change the data into float data type, and remove the '$'

#### Create your a dataframe

Create dataframe using dictionary of lists

{% highlight python%}
raw_data = {'first_name': ['Jason', 'Molly', 'Tina', 'Jake', 'Amy'],
        'last_name': ['Miller', 'Jacobson', ".", 'Milner', 'Cooze'],
        'age': [42, 52, 36, 24, 73],
        'preTestScore': [4, 24, 31, ".", "."],
        'postTestScore': ["25,000", "94,000", 57, 62, 70]}
df = pd.DataFrame(raw_data, columns = ['first_name', 'last_name', 'age', 'preTestScore', 'postTestScore'])
{% endhighlight %}

#### Dump data to csv

Firstly, what is your working directory?

{% highlight python%} 
import os
os.getcwd()
os.chdir('/Users/shengqiu/Dropbox')
{% endhighlight %}

Then dump the csv to the directory you desire. 

- The separation is default to be  `','`, 
-  `mode = "a"` means append to the exsiting; `mode = 'w'` will overwrite
-  `header` enable loading the theader as well
-  `encodeing` can be set to 'ascii' or 'utf-8'
-  `to_json` are available as well

{% highlight python%} 
df.to_csv(path_or_buf="yelp/dd.csv", sep=',', header=True, mode = 'a', quotechar='"',line_terminator='\n')
{% endhighlight %}

#### Clipboard!!!

The clipboard works well in python 3.5 (The version I am using). However, in python 2.7, there might be problem because of text encoding. The encoding is essentially why I prefer python3 over python2.

{% highlight python%} 
hank = pd.read_clipboard()
{% endhighlight %}

---

## Work with data structure

This part uses the dataset <a href="http://grouplens.org/datasets/movielens/">movie dataset</a>, follows this instruction <a href="http://www.gregreda.com/2013/10/26/working-with-pandas-dataframes/"> Greg Reda's Tutorial </a>

{% highlight python%} 
# users
u_cols = ['user_id', 'age', 'sex', 'occupation', 'zip_code']
users = pd.read_csv('ml-100k/u.user', sep='|', names=u_cols)

# ratings
r_cols = ['user_id', 'movie_id', 'rating', 'unix_timestamp']
ratings = pd.read_csv('ml-100k/u.data', sep='\t', names=r_cols)

# movie
m_cols = ['movie_id', 'title', 'release_date', 'video_release_date', 'imdb_url']
movies = pd.read_csv('ml-100k/u.item', sep='|', names=m_cols, usecols=range(5),encoding = 'latin-1')
{% endhighlight %}

#### Firstly, let's get some information

It is important to understand the data roughly to begin, especially data type. The `.info()` method is pretty cool because it tells you how many **non-null** cells there are.

{% highlight python%} 
movie? # detailed explaination of the datatype
movies.info() # datatype of each column
movies.dtypes # similar to the previous
movies.describe() # summary of numeric columns
movies.head(50) # first 50 rows
movies['title'].tail(20) # last 30 rows of the 'title' column
{% endhighlight %}

#### Format the index

Index could be given in the dataset already. So there is a way format the index.

{% highlight python%} 
# Replace the meaningless index with the 'movie_id', inplace means don't make a copy
movies.set_index('movie_id',inplace = True)

# Or put it back
users.reset_index(inplace=True)
{% endhighlight %}

---

## Referance or Create a copy

Before we go deep into it... Python does some thing called referance assignment. This means no physical location is allocated to store the variable . In stead, a variable is just a name or a pointer; the value is stored in somewhere else. This is not only in pandas, but also for all python functions/scripts/classes... Here are some other <a href="http://shengqiu.github.io/python/1000/01/01/hahaha-wtf.html">funny stuff  </a>in python.

#### Referance

So if you do sth like this

{% highlight python%} 
df = pd.DataFrame([[1], [2], [3]])
df2 = df
df[0][1] = 1000
{% endhighlight %}

`df2` will change as well even you didn't change `df2` directly. This is all because of the referance assignment. So this could be problematic if you are not aware of it...

#### Create a copy

But if you do this, which is a deep copy, you are fine.

{% highlight python%} 
df2 = df.copy(deep=True)
df[0][1] = 1000
{% endhighlight %}

This is deepy copy cut the linkage between `df2` and `df`, because a seperate phisical location is created to store `df2`.... not exactly, but somewhat like that...


---

## Row and column operations

#### Add column in pandas

{% highlight python%} 
movies['year'] = Series(str(movies.release_date), index=range(len(movies.index)))
{% endhighlight %}


#### nan means it is not a number

{% highlight python%} 
import math
x=float('nan')
math.isnan(x)
{% endhighlight %}

This is really funny...

{% highlight python%} 
def isNaN(num):
    return num != num
{% endhighlight %}

check if one column contains `nan`, and return the array of logic statements

{% highlight python%} 
df2['one'].isnull() # or
pd.isnull(df2['one'])
df2['four'].notnull()

{% endhighlight %}

#### Filter-out the rows with `nan`

`nan` means not a number. It is really annoying, so I just want to get rid of it...

{% highlight python%} 
movies['year'] = Series(str(movies.release_date), index=range(len(movies.index)))
{% endhighlight %}

`nan` is pretty funny, and so is `None`, you can check the other post I did.

<a href="http://shengqiu.github.io/python/1000/01/01/hahaha-wtf.html">hahaha wtf python?</a>

#### Coarse the column to string

First coarse to string and check all date-time are well formated. So I found that there are 'nan', so have to deal with it.

{% highlight python%} 
movies_temp = movies.copy(deep = True)
movies_temp['year'] = movies_temp['release_date'].astype(str)
movies_temp = movies_temp[:][movies_temp['year'] != 'nan']
movies_temp['year'] = [one.split("-")[2] for one in movies_temp['year']]
movies_temp['year']=movies_temp['year'].astype(int)
{% endhighlight %}

Now the new column `movies_temp['year']` is year in integer datatype.
 
#### Coarse the column to datetime

Pandas support native datetime objects. It uses the `NumPy datetime64 dtype` 

{% highlight python%} 
movies_temp = movies.copy(deep = True)
time_temp = pd.DatetimeIndex(movies_temp['release_date'])
movies_temp['year'] = pd.Series(time_temp.year.astype(int))
{% endhighlight %}

Now this looks pretty neat. But if I start with this appraoch, I won't be able to capture the `nan`. So I prefer the string approach, which go back to the raw format and covert back.

---


## `Apply` and `Map`

3. Since you are using pandas already, use more `apply` and `map`

---

# Reference

<a href="http://1.aisensiy.sinaapp.com/2014/03/%E6%9C%80%E8%BF%91%E4%BD%BF%E7%94%A8-pandas-%E7%9A%84%E6%80%BB%E7%BB%93/">reference 1</a>

<a href="http://docs.python-guide.org/en/latest/">reference 2</a>

<a href="http://www.gregreda.com/2013/10/26/intro-to-pandas-data-structures/">reference 2</a>
