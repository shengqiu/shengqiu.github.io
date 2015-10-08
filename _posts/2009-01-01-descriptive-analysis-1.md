---
layout: post
title:  "Decriptive Analysis 1"
date:   2009-01-01 14:22:19
categories: yelp_project
---

---
	
# Import the database

{% highlight python%}	
from pymongo import MongoClient
client = MongoClient('localhost', 27017)
db = client.yelp
biz = db.businesses
checkin = db.checkins
reviews = db.reviews
tips = db.tips
users = db.users
{% endhighlight %}


---

#  How many business are there in each city?

Plot # of business in each city.

{% highlight python%}	

from pymongo import MongoClient
from bson.son import SON
import plotly.plotly as py
from plotly.graph_objs import *


def getKey(item):
    return item[2]

pipeline = [
    {"$group": {"_id": {'city':"$city", 'state': '$state'}, "count": {"$sum": 1}}},
    {"$sort": SON([("count", -1), ("_id", -1)])}
    ]
    
city_list= list(biz.aggregate(pipeline))

city_list_new = [
   [str(one_city['_id']['city'].encode('utf8')), 
   str(one_city['_id']['state'].encode('utf8')), 
   one_city['count'] ]
   for one_city in city_list]

city_list_sorted = sorted(city_list_new, key=getKey, reverse = True)

# encoding screwed Montreal up
city_list_sorted[12][2]=city_list_sorted[12][2]+city_list_sorted[9][2]
del city_list_sorted[9][2]
city_list_sorted = sorted(city_list_sorted, key=getKey, reverse = True)


data = Data([
    Bar(
        x = [one_city[0] for one_city in city_list_sorted] ,
        y= [one_city[2] for one_city in city_list_sorted]
    )
])
plot_url = py.plot(data, filename='biz plot')
{% endhighlight %}

<div>
    <a href="https://plot.ly/~FrankQiu/17/" target="_blank" title="" style="display: block; text-align: center;"><img src="https://plot.ly/~FrankQiu/17.png" alt="" style="max-width: 100%;width: 600px;"  width="600" onerror="this.onerror=null;this.src='https://plot.ly/404.png';" /></a>
    <script data-plotly="FrankQiu:17"  src="https://plot.ly/embed.js" async></script>
</div>


So we can see that there are the # of business differs a lot among cities.


list of cities having more than 5000 businesses
{% highlight python%}
['Las Vegas', 'NV', 27200]
['Phoenix', 'AZ', 16820]
['Charlotte', 'NC', 8448]
['Scottsdale', 'AZ', 8078]
['Montreal', 'QC', 6508]
['Edinburgh', 'EDH', 5860]
['Pittsburgh', 'PA', 5448]
{% endhighlight %}

<div>
    <a href="https://plot.ly/~FrankQiu/20/" target="_blank" title="" style="display: block; text-align: center;"><img src="https://plot.ly/~FrankQiu/20.png" alt="" style="max-width: 100%;width: 600px;"  width="600" onerror="this.onerror=null;this.src='https://plot.ly/404.png';" /></a>
    <script data-plotly="FrankQiu:20"  src="https://plot.ly/embed.js" async></script>
</div>


# How many biz are there in each state?

Plot of businesses in each state (26 states in total)

following code change the state code from abbreviation to full name:


{% highlight python%}

state_code = """
Alabama AL
Alaska  AK
Arizona AZ
Arkansas  AR
California  CA
Colorado  CO
Connecticut CT
Delaware  DE
Florida FL
Georgia GA
Hawaii  HI
Idaho ID
Illinois  IL
Indiana IN
Iowa  IA
Kansas  KS
Kentucky  KY
Louisiana LA
Maine ME
Maryland  MD
Massachusetts MA
Michigan  MI
Minnesota MN
Mississippi MS
Missouri  MO
Montana MT
Nebraska  NE
Nevada  NV
New Hampshire NH
New Jersey  NJ
New Mexico  NM
New York  NY
North Carolina  NC
North Dakota  ND
Ohio  OH
Oklahoma  OK
Oregon  OR
Pennsylvania  PA
Rhode Island  RI
South Carolina  SC
South Dakota  SD
Tennessee TN
Texas TX
Utah  UT
Vermont VT
Virginia  VA
Washington  WA
West Virginia WV
Wisconsin WI
Wyoming WY
Alberta AB
British Columbia  BC
Manitoba  MB
New Brunswick NB
Newfoundland and Labrador NL
Nova Scotia NS
Northwest Territories NT
Nunavut NU
Ontario ON
Prince Edward Island  PE
Quebec  QC
Saskatchewan  SK
Yukon YT
"""

state_lines = state_code.split('\n')
state_dict = {state_line.split('\t')[1]: state_line.split('\t')[0] for state_line in state_lines[1:-1]}

for city in city_list_sorted:
    if city[0] in state_dict:
        name_temp = state_dict[city[0]]
        city[0] = name_temp



{% endhighlight %}


<div>
    <a href="https://plot.ly/~FrankQiu/70/" target="_blank" title="" style="display: block; text-align: center;"><img src="https://plot.ly/~FrankQiu/70.png" alt="" style="max-width: 100%;width: 600px;"  width="600" onerror="this.onerror=null;this.src='https://plot.ly/404.png';" /></a>
    <script data-plotly="FrankQiu:70"  src="https://plot.ly/embed.js" async></script>
</div>


{% highlight python%}
['Arizona', 50460]
['Nevada', 32970]
['North Carolina', 9926]
['Quebec', 7842]
['Pennsylvania', 6082]
['EDH', 5942]
['Wisconsin', 4614]
['BW', 1868]
['Illinois', 1254]
['Ontario', 702]
['South Carolina', 378]
['MLN', 246]
['RP', 26]
['ELN', 20]
['FIF', 8]
['SCB', 6]
['California', 6]
['XGL', 2]
['Washington', 2]
['Oregon', 2]
['NW', 2]
['NTH', 2]
['Minnesota', 2]
['Massachusetts', 2]
['KHL', 2]
['HAM', 2]
{% endhighlight %}

It is a bit suprising to see Arizona (AZ), since even Pheonix is not even a big city...
So plot cities in Phoenix

<div>
    <a href="https://plot.ly/~FrankQiu/37/" target="_blank" title="" style="display: block; text-align: center;"><img src="https://plot.ly/~FrankQiu/37.png" alt="" style="max-width: 100%;width: 600px;"  width="600" onerror="this.onerror=null;this.src='https://plot.ly/404.png';" /></a>
    <script data-plotly="FrankQiu:37"  src="https://plot.ly/embed.js" async></script>
</div>

The top 10 high cities in phoenix

<div>
    <a href="https://plot.ly/~FrankQiu/49/" target="_blank" title="" style="display: block; text-align: center;"><img src="https://plot.ly/~FrankQiu/49.png" alt="" style="max-width: 100%;width: 600px;"  width="600" onerror="this.onerror=null;this.src='https://plot.ly/404.png';" /></a>
    <script data-plotly="FrankQiu:49"  src="https://plot.ly/embed.js" async></script>
</div>

{% highlight python %}
['Phoenix', 16820]
['Scottsdale', 8078]
['Mesa', 4694]
['Tempe', 4516]
['Chandler', 3734]
['Glendale', 2754]
['Gilbert', 2526]
['Peoria', 1376]
['Surprise', 896]
['Goodyear', 708]
{% endhighlight %}


Do the same things for Nevada:

<div>
    <a href="https://plot.ly/~FrankQiu/54/" target="_blank" title="" style="display: block; text-align: center;"><img src="https://plot.ly/~FrankQiu/54.png" alt="" style="max-width: 100%;width: 600px;"  width="600" onerror="this.onerror=null;this.src='https://plot.ly/404.png';" /></a>
    <script data-plotly="FrankQiu:54"  src="https://plot.ly/embed.js" async></script>
</div>


So there are a lot of business in Las Vegas, but there are very few in the rest of Nevada


---

# how do the user activeness differ among different cities?

plot all cities:


<div>
    <a href="https://plot.ly/~FrankQiu/62/" target="_blank" title="" style="display: block; text-align: center;"><img src="https://plot.ly/~FrankQiu/62.png" alt="" style="max-width: 100%;width: 600px;"  width="600" onerror="this.onerror=null;this.src='https://plot.ly/404.png';" /></a>
    <script data-plotly="FrankQiu:62"  src="https://plot.ly/embed.js" async></script>
</div>


plot top 30 cities

<div>
    <a href="https://plot.ly/~FrankQiu/65/" target="_blank" title="" style="display: block; text-align: center;"><img src="https://plot.ly/~FrankQiu/65.png" alt="" style="max-width: 100%;width: 600px;"  width="600" onerror="this.onerror=null;this.src='https://plot.ly/404.png';" /></a>
    <script data-plotly="FrankQiu:65"  src="https://plot.ly/embed.js" async></script>
</div>


{% highlight python %}
['Summerlin', 149.0]
['Lower Lawrenceville', 139.0]
['Black Canyon City', 133.0]
['North Scottsdale', 106.0]
['Sedona', 93.0]
['Goldfield', 93.0]
['Pittsburgh/Waterfront', 73.0]
['Phoenix-Ahwatukee', 70.0]
['N. Las Vegas', 64.5]
['Las Vegas', 50.37056098816264]
['Green Tree', 50.0]
['Lawrenceville', 48.5]
['Henderson (Stephanie)', 43.0]
['Spring Valley', 35.77777777777778]
['Lake Wylie', 35.666666666666664]
['Glendale Az', 34.0]
['Tortilla Flat', 33.666666666666664]
['W Henderson', 33.0]
['Scottsdale', 32.10918544194107]
['Ahwatukee', 31.9]
['West Homestead', 31.25]
['Henderson (Green  Valley)', 31.0]
['Tempe', 30.858281665190432]
['Clark County', 29.4]
['San Diego', 29.0]
['Pittsburgh/S. Hills Galleria', 29.0]
['Brookline', 29.0]
['Phoenix', 28.24768133174792]
['North Queensferry', 27.0]
['Mesa ', 27.0]
{% endhighlight %}


It is pretty interesting to see:

- Las vegas is the 10th
- Pittsburg is 25th
- Phoenix is 27th

So it is not necessary to say that big cities are more active









