---
layout: post
title:  "hahaha wtf Python?"
date:   1000-01-01 00:00:00
categories: python
---

# do the following

Do the following you will get an infinite loop in `values`

{% highlight python%} 
values=[0,1,2]
values[1] = values
values
{% endhighlight %} 



# And do the following

Do the following you can change `a` without changing `a`.

{% highlight python%} 
a = [1, 2, 3, 4]
b = a
b[2] = 1000
{% endhighlight %} 

When I first saw it I was like 'hahaha wtf'. So basically, this is because python creates `[1,2,3,4]` and then reference both a and b to `[1,2,3,4]`. If b is changed, the `[1,2,3,4]` is changed.