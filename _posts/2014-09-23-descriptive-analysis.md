---
layout: post
title:  "Descriptive Analysis"
date:   2014-09-23 14:22:19
categories: yelp_project
---

# Analysis of food related tags:
There are 8047 kinds of combination of tags:

{% highlight python %}

[{'_id': ['Mexican', 'Restaurants'], 'count': 1481},
 {'_id': ['Pizza', 'Restaurants'], 'count': 1068},
 {'_id': ['Hotels & Travel', 'Event Planning & Services', 'Hotels'],
  'count': 982},
 {'_id': ['Food', 'Coffee & Tea'], 'count': 958},
 {'_id': ['Chinese', 'Restaurants'], 'count': 934},
 {'_id': ['Beauty & Spas', 'Nail Salons'], 'count': 883},
 {'_id': ['Restaurants', 'Italian'], 'count': 674},
 {'_id': ['Hair Salons', 'Beauty & Spas'], 'count': 651},
 {'_id': ['Food', 'Grocery'], 'count': 585},
 {'_id': ['Burgers', 'Fast Food', 'Restaurants'], 'count': 582},
 ...]
{% endhighlight %}

There are 783 kinds of tags in total:

{% highlight python %}
[('Restaurants', 21892),
 ('Shopping', 8919),
 ('Food', 7862),
 ('Beauty & Spas', 4738),
 ('Nightlife', 4340),
 ('Bars', 3628),
 ('Health & Medical', 3213),
 ('Automotive', 2965),
 ('Home Services', 2853),
 ('Fashion', 2566),
 ...]
{% endhighlight %}

# Analysis of Review Volume over time by category

The total number of reviews by each categories

<div>
    <a href="https://plot.ly/~FrankQiu/184/" target="_blank" title="" style="display: block; text-align: center;"><img src="https://plot.ly/~FrankQiu/184.png" alt="" style="max-width: 100%;width: 600px;"  width="600" onerror="this.onerror=null;this.src='https://plot.ly/404.png';" /></a>
    <script data-plotly="FrankQiu:184"  src="https://plot.ly/embed.js" async></script>
</div>

All reviews over time:

<div>
    <a href="https://plot.ly/~FrankQiu/220/" target="_blank" title="" style="display: block; text-align: center;"><img src="https://plot.ly/~FrankQiu/220.png" alt="" style="max-width: 100%;width: 600px;"  width="600" onerror="this.onerror=null;this.src='https://plot.ly/404.png';" /></a>
    <script data-plotly="FrankQiu:220"  src="https://plot.ly/embed.js" async></script>
</div>

---

All reviews about Mexican restaurant over time

<div>
    <a href="https://plot.ly/~FrankQiu/189/" target="_blank" title="" style="display: block; text-align: center;"><img src="https://plot.ly/~FrankQiu/189.png" alt="" style="max-width: 100%;width: 600px;"  width="600" onerror="this.onerror=null;this.src='https://plot.ly/404.png';" /></a>
    <script data-plotly="FrankQiu:189"  src="https://plot.ly/embed.js" async></script>
</div>

---

Normalized number of reviews about Mexican restaurant over time:

<div>
    <a href="https://plot.ly/~FrankQiu/224/" target="_blank" title="" style="display: block; text-align: center;"><img src="https://plot.ly/~FrankQiu/224.png" alt="" style="max-width: 100%;width: 600px;"  width="600" onerror="this.onerror=null;this.src='https://plot.ly/404.png';" /></a>
    <script data-plotly="FrankQiu:224"  src="https://plot.ly/embed.js" async></script>
</div>

---

Total number of review over the year. 

1. So we can see valley on:

- Valentine's Day
- Feb 29
- July 4th
- Holloween
- Nov 27/ Nov 28 (around Thanksgiving)
- Christmas

2. right after the holiday/vacation/fesitival, we always have a 'after spike', for almost every valley (except for thanksgiving, holloween)
3. We can also see peak right after Christmas to Jan 08
4. The rest of Jan is low
5. Summer (Jun, July, Aug, early Sept) have higher volume than rest of the year, except for the christmas holiday spike.

<div>
    <a href="https://plot.ly/~FrankQiu/229/" target="_blank" title="" style="display: block; text-align: center;"><img src="https://plot.ly/~FrankQiu/229.png" alt="" style="max-width: 100%;width: 600px;"  width="600" onerror="this.onerror=null;this.src='https://plot.ly/404.png';" /></a>
    <script data-plotly="FrankQiu:229"  src="https://plot.ly/embed.js" async></script>
</div>

---

There is a similar patern in the volume of mexican reviews over time

<div>
    <a href="https://plot.ly/~FrankQiu/192/" target="_blank" title="" style="display: block; text-align: center;"><img src="https://plot.ly/~FrankQiu/192.png" alt="" style="max-width: 100%;width: 600px;"  width="600" onerror="this.onerror=null;this.src='https://plot.ly/404.png';" /></a>
    <script data-plotly="FrankQiu:192"  src="https://plot.ly/embed.js" async></script>
</div>

---

This is what it looks like after normalize it... pretty much it is white noise

1. May 5th is Cinco de Mayo, which is the Mexican Independence Day.

<div>
    <a href="https://plot.ly/~FrankQiu/234/" target="_blank" title="" style="display: block; text-align: center;"><img src="https://plot.ly/~FrankQiu/234.png" alt="" style="max-width: 100%;width: 600px;"  width="600" onerror="this.onerror=null;this.src='https://plot.ly/404.png';" /></a>
    <script data-plotly="FrankQiu:234"  src="https://plot.ly/embed.js" async></script>
</div>

---

The pattern for ice cream is different:

Firstly the total volume:

<div>
    <a href="https://plot.ly/~FrankQiu/202/" target="_blank" title="" style="display: block; text-align: center;"><img src="https://plot.ly/~FrankQiu/202.png" alt="" style="max-width: 100%;width: 600px;"  width="600" onerror="this.onerror=null;this.src='https://plot.ly/404.png';" /></a>
    <script data-plotly="FrankQiu:202"  src="https://plot.ly/embed.js" async></script>
</div>

Then Normalize it:

<div>
    <a href="https://plot.ly/~FrankQiu/238/" target="_blank" title="" style="display: block; text-align: center;"><img src="https://plot.ly/~FrankQiu/238.png" alt="" style="max-width: 100%;width: 600px;"  width="600" onerror="this.onerror=null;this.src='https://plot.ly/404.png';" /></a>
    <script data-plotly="FrankQiu:238"  src="https://plot.ly/embed.js" async></script>
</div>

---

Normalized italian

<div>
    <a href="https://plot.ly/~FrankQiu/241/" target="_blank" title="" style="display: block; text-align: center;"><img src="https://plot.ly/~FrankQiu/241.png" alt="" style="max-width: 100%;width: 600px;"  width="600" onerror="this.onerror=null;this.src='https://plot.ly/404.png';" /></a>
    <script data-plotly="FrankQiu:241"  src="https://plot.ly/embed.js" async></script>
</div>

---

Normalized Amrican

<div>
    <a href="https://plot.ly/~FrankQiu/249/" target="_blank" title="" style="display: block; text-align: center;"><img src="https://plot.ly/~FrankQiu/249.png" alt="" style="max-width: 100%;width: 600px;"  width="600" onerror="this.onerror=null;this.src='https://plot.ly/404.png';" /></a>
    <script data-plotly="FrankQiu:249"  src="https://plot.ly/embed.js" async></script>
</div>

---

Normalized Night Life

<div>
    <a href="https://plot.ly/~FrankQiu/246/" target="_blank" title="" style="display: block; text-align: center;"><img src="https://plot.ly/~FrankQiu/246.png" alt="" style="max-width: 100%;width: 600px;"  width="600" onerror="this.onerror=null;this.src='https://plot.ly/404.png';" /></a>
    <script data-plotly="FrankQiu:246"  src="https://plot.ly/embed.js" async></script>
</div>


# Analysis of Review score over time by category

Plot mexican star rating over time:

<div>
    <a href="https://plot.ly/~FrankQiu/262/" target="_blank" title="" style="display: block; text-align: center;"><img src="https://plot.ly/~FrankQiu/262.png" alt="" style="max-width: 100%;width: 600px;"  width="600" onerror="this.onerror=null;this.src='https://plot.ly/404.png';" /></a>
    <script data-plotly="FrankQiu:262"  src="https://plot.ly/embed.js" async></script>
</div>

MA(30) plot
<div>
    <a href="https://plot.ly/~FrankQiu/272/" target="_blank" title="" style="display: block; text-align: center;"><img src="https://plot.ly/~FrankQiu/272.png" alt="" style="max-width: 100%;width: 600px;"  width="600" onerror="this.onerror=null;this.src='https://plot.ly/404.png';" /></a>
    <script data-plotly="FrankQiu:272"  src="https://plot.ly/embed.js" async></script>
</div>


Plot star rating of mexican over the year:

<div>
    <a href="https://plot.ly/~FrankQiu/266/" target="_blank" title="" style="display: block; text-align: center;"><img src="https://plot.ly/~FrankQiu/266.png" alt="" style="max-width: 100%;width: 600px;"  width="600" onerror="this.onerror=null;this.src='https://plot.ly/404.png';" /></a>
    <script data-plotly="FrankQiu:266"  src="https://plot.ly/embed.js" async></script>
</div>

MA(3) plot

<div>
    <a href="https://plot.ly/~FrankQiu/284/" target="_blank" title="" style="display: block; text-align: center;"><img src="https://plot.ly/~FrankQiu/284.png" alt="" style="max-width: 100%;width: 600px;"  width="600" onerror="this.onerror=null;this.src='https://plot.ly/404.png';" /></a>
    <script data-plotly="FrankQiu:284"  src="https://plot.ly/embed.js" async></script>
</div>











