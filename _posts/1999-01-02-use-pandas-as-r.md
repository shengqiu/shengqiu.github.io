---
layout: post
title:  "Pandas Short Tutorial - Pandas is like SQL"
date:   1999-01-02 00:00:00
categories: python2r
---

---

## Joining in pandas

Do join like SQL by changing how into "left", "right", "inner", "outer"

{% highlight python%} 
pd.merge(left_frame, right_frame, on='key', how='outer')
{% endhighlight %}

---


## Groupby in pandas