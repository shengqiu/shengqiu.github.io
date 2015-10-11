---
layout: post
title:  "Pandas Short Tutorial - Pandas is like SQL"
date:   1999-01-02 00:00:00
categories: python
---

- Pandas makes python like SQL, which enables a lot of `GROUPBY` and `JOIN` like SQL
- This tutorial is based on python 3.4 and pandas 0.16.2
- Also take a look at the other post: <a href="http://shengqiu.github.io/python2r/1999/01/01/use-python-as-r.html">Pandas is like R</a>

---

## JOIN

Do join like SQL by changing how into "left", "right", "inner", "outer. That's just this simple...

#### Create two tables

{% highlight python%} 
left_frame = pd.DataFrame({'key': range(5), 'left_value': ['a', 'b', 'c', 'd', 'e']}
{% endhighlight %}

| key 	| left_value 	|
|-----	|------------	|
| 4   	| e          	|
| 3   	| d          	|
| 2   	| c          	|
| 1   	| b          	|
| 0   	| a          	|

{% highlight python%} 
right_frame = pd.DataFrame({'key': range(2, 7), 'right_value': ['f', 'g', 'h', 'i', 'j']}
{% endhighlight %}

| key 	| right_value 	|
|-----	|-------------	|
| 2   	| f           	|
| 3   	| g           	|
| 4   	| h           	|
| 5   	| i           	|
| 6   	| j           	|

#### Inner JOIN

{% highlight python%} 
pd.merge(left_frame, right_frame, on='key', how='inner')
{% endhighlight %}


| key 	| left_value 	| right_value 	|
|-----	|------------	|-------------	|
| 0.0 	| a          	| null        	|
| 1.0 	| b          	| null        	|
| 2.0 	| c          	| f           	|
| 3.0 	| d          	| g           	|
| 4.0 	| e          	| h           	|
| 5.0 	| null       	| i           	|
| 6.0 	| null       	| j           	|

---

## UNION / rbind / cbind

#### Combine verticlly, rbind

{% highlight python%} 
pd.concat([left_frame, right_frame])
{% endhighlight%} 

|   	| key 	| left_value 	| right_value 	|
|---	|-----	|------------	|-------------	|
| 0 	| 0   	| a          	| null         	|
| 1 	| 1   	| b          	| null         	|
| 2 	| 2   	| c          	| null         	|
| 3 	| 3   	| d          	| null         	|
| 4 	| 4   	| e          	| null         	|
| 0 	| 2   	| null        	| f           	|
| 1 	| 3   	| null        	| g           	|
| 2 	| 4   	| null        	| h           	|
| 3 	| 5   	| null        	| i           	|
| 4 	| 6   	| null        	| j           	|

#### Combine horizontally, cbind

{% highlight python%} 
pd.concat([left_frame, right_frame], axis=1)
{% endhighlight%} 

| key | left_value	| key 	| right_value 	|
|-----|-------------|-----	|-----------	|
| 0   | a   		| 2     | f 			|
| 1   | b   		| 3    	| g 			|
| 2   | c   		| 4     | h 			|
| 3   | d   		| 5     | i 			|
| 4   | e   		| 6     | j 			|


---

## GROUPBY







