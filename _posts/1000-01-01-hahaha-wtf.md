---
layout: post
title:  "hahaha wtf Python?"
date:   1000-01-01 00:00:00
categories: python
---



---

## Variable reference 

#### Do the following

Do the following you will get an infinite loop in `values`

{% highlight python%} 
values=[0,1,2]
values[1] = values
values
{% endhighlight %} 

#### And do the following

Do the following you can change `a` without changing `a`.

{% highlight python%} 
a = [1, 2, 3, 4]
b = a
b[2] = 1000
{% endhighlight %} 

The output is `[1,[...],4]`

When I first saw it I was like 'hahaha wtf'. So basically, this is because python creates `[1,2,3,4]` and then reference both a and b to `[1,2,3,4]`. If b is changed, the `[1,2,3,4]` is changed.

---

## `nan` and `None`

`None` means it is empty. In each python interpreter session, a `None` object will be created, and when `this = None`, `this` got assigned to the object. Interestingly, in Spyder, if you do `this = None`, then `this` will disappear from the variable explorer viewer. This is the same thing as the `Null` in SQL.

`nan` means not a number. And something like this

{% highlight python%} 
myarr[myarr == np.nan] = 0. # doesn't work
{% endhighlight %} 

will not ever work. So have to do the following:

{% highlight python%} 
myarr[np.isnan(myarr)]
{% endhighlight %} 

Some funny stuff...

{% highlight python%} 
this = None
that = numpy.nan
this is this # True
that is that # True
this == this # True
that == that # False
that != that # True
{% endhighlight %} 














