---
layout: post
title:  "The first package is pandas"
date:   1999-01-01 00:00:00
categories: python2r
---


- Pandas makes python like R, which enables a lot of basic operations that R can do.
	
--- 

## Even before going to dataframe, firstly we can check out the pandas series

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

## load data frame from csv

The chunksize parameter defines how many lines in total

{% highlight python%} 
import pandas as pd
df = pd.read_csv('test.csv', chunksize=10000)
{% endhighlight %}

Another really cool example

{% highlight python%} 
headers = ['name', 'title', 'department', 'salary']
chicago = pd.read_csv('city-of-chicago-salaries.csv',header=False,names=headers,converters={'salary': lambda x: float(x.replace('$', ''))})
{% endhighlight %}

Here `lambda x: float(x.replace('$',''))` change the data into float data type, and remove the '$'

---

## Create your a dataframe

Create dataframe using dictionary of lists

{% highlight python%}
raw_data = {'first_name': ['Jason', 'Molly', 'Tina', 'Jake', 'Amy'],
        'last_name': ['Miller', 'Jacobson', ".", 'Milner', 'Cooze'],
        'age': [42, 52, 36, 24, 73],
        'preTestScore': [4, 24, 31, ".", "."],
        'postTestScore': ["25,000", "94,000", 57, 62, 70]}
df = pd.DataFrame(raw_data, columns = ['first_name', 'last_name', 'age', 'preTestScore', 'postTestScore'])
df
{% endhighlight %}

---

## Dump data to csv

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

---

## Clipboard!!!

The clipboard works well in python 3.5 (The version I am using). However, in python 2.7, there might be problem because of text encoding. The encoding is essentially why I prefer python3 over python2.

{% highlight python%} 
hank = pd.read_clipboard()
{% endhighlight %}

---

## work with data structure

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
movies = pd.read_csv('ml-100k/u.item', sep='|', names=m_cols, usecols=range(5))
{% endhighlight %}

---

## Firstly, let's get some information

It is important to understand the data roughly to begin, especially data type. The `.info()` method is pretty cool because it tells you how many **non-null** cells there are.

{% highlight python%} 
movie? # detailed explaination of the datatype
movies.info() # datatype of each column
movies.dtypes # similar to the previous
movies.describe() # summary of numeric columns
movies.head(50) # first 50 rows
movies['title'].tail(20) # last 30 rows of the 'title' column
{% endhighlight %}

---

## some formating the index

Index could be given in the dataset already. So there is a way format the index.

{% highlight python%} 
# Replace the meaningless index with the 'movie_id', inplace means don't make a copy
movies.set_index('movie_id',inplace = True)

# Or put it back
users.reset_index(inplace=True)
{% endhighlight %}

---

## Copy or Replace

Before we go deep into it... Python does some thin called 

---

## Coarse some column into another datatype

Here I want to aggregate by year, so I tried two ways:

#### Coarse the column to string

This works well when all date-time are well formated. But some time there are 'nan', so have to deal with it.

{% highlight python%} 
movies['year'] = movies['release_date'].astype(str)
movies = movies.loc[movies['year'] != 'nan',]
{% endhighlight %}

 
#### Coarse the column to datetime

{% highlight python%} 

{% endhighlight %}

---

## None, nan, and other annoying stuff....

nan means it is not a number

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

---

## Filter-out the rows with `None` or `nan`

`None` and `nan` are really annoying, so I just want to get rid of them...

{% highlight python%} 
movies['year'] = Series(str(movies.release_date), index=range(len(movies.index)))
{% endhighlight %}

---

## add column in pandas

{% highlight python%} 
movies['year'] = Series(str(movies.release_date), index=range(len(movies.index)))
{% endhighlight %}

---

## Joining in pandas

Do join like SQL by changing how into "left", "right", "inner", "outer"

{% highlight python%} 
pd.merge(left_frame, right_frame, on='key', how='outer')
{% endhighlight %}

---


## Groupby in pandas



3. Since you are using pandas already, use more `apply` and `map`

---

<a href="http://1.aisensiy.sinaapp.com/2014/03/%E6%9C%80%E8%BF%91%E4%BD%BF%E7%94%A8-pandas-%E7%9A%84%E6%80%BB%E7%BB%93/">reference 1</a>

<a href="http://docs.python-guide.org/en/latest/">reference 2</a>

<a href="http://www.gregreda.com/2013/10/26/intro-to-pandas-data-structures/">reference 2</a>
