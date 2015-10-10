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

## work with data structure

{% highlight python%} 
hank = pd.read_clipboard()
{% endhighlight %}

This part uses the dataset <a href="http://grouplens.org/datasets/movielens/">movie dataset</a>, follows this instruction <a href="http://www.gregreda.com/2013/10/26/working-with-pandas-dataframes/"> Greg Reda's Tutorial </a>

## Firstly, let's get some informat

{% highlight python%} 
movie? # detailed explaination of the datatype
movies.info() # datatype of each column
movies.dtypes # similar to the previous
movies.describe() # summary of numeric columns
movies.head(50) # first 50 rows
movies['title'].tail(20) # last 30 rows of the 'title' column
{% endhighlight %}








3. Since you are using pandas already, use more `apply` and `map`

---


http://1.aisensiy.sinaapp.com/2014/03/%E6%9C%80%E8%BF%91%E4%BD%BF%E7%94%A8-pandas-%E7%9A%84%E6%80%BB%E7%BB%93/

http://docs.python-guide.org/en/latest/

http://www.gregreda.com/2013/10/26/intro-to-pandas-data-structures/