---
layout: post
title:  "Decriptive Analysis of Business Collection"
date:   2009-01-02 00:00:00
categories: yelp_project
---

---
	
# According to the database


{% highlight python%}   
{
    'type':     'business',
    'business_id': (encrypted business id),
    'name': (business name),
    'neighborhoods': [(hood names)],
    'full_address': (localized address),
    'city': (city),
    'state': (state),
    'latitude': latitude,
    'longitude': longitude,
    'stars': (star rating, rounded to half-stars),
    'review_count': review count,
    'categories': [(localized category names)]
    'open': True / False (corresponds to closed, not business hours),
    'hours': {
        (day_of_week): {
            'open': (HH:MM),
            'close': (HH:MM)
        },
        ...
    },
    'attributes': {
        (attribute_name): (attribute_value),
        ...
    },
}

{% endhighlight %}

---

# **Franchise**

#### This is the plot of # of reviews for each biz
<div>
    <a href="https://plot.ly/~FrankQiu/110/" target="_blank" title="" style="display: block; text-align: center;"><img src="https://plot.ly/~FrankQiu/110.png" alt="" style="max-width: 100%;width: 600px;"  width="600" onerror="this.onerror=null;this.src='https://plot.ly/404.png';" /></a>
    <script data-plotly="FrankQiu:110"  src="https://plot.ly/embed.js" async></script>
</div>

#### So mostly are local brands, non-franchise. Following is the rank of some franchise brands


|  Brank     | Review | Rank |
|------------|--------|------|
|  Starbucks | 6481   | 1    |
|  In-N-Out  | 2955   | 9    |
|  Chipotle  | 2759   | 10    |
|  Mcdonald  | 2334   |19    |
|  Five Guys | 2037   |34    |
|  Walmart   | 1581   |50    |
|  Subway    | 1562   |52    |
|Olive Garden| 1466   |65    |
| P.F. Change| 1422   |70    |



#### If we do #review/#store, we get:




<div>
    <a href="https://plot.ly/~FrankQiu/118/" target="_blank" title="" style="display: block; text-align: center;"><img src="https://plot.ly/~FrankQiu/118.png" alt="" style="max-width: 100%;width: 600px;"  width="600" onerror="this.onerror=null;this.src='https://plot.ly/404.png';" /></a>
    <script data-plotly="FrankQiu:118"  src="https://plot.ly/embed.js" async></script>
</div>


| Brank     | Review per store| Rank |
|-----------|--------|------|
| Starbucks | 15  | 14740    |
| In-N-Out  | 98  | 2693    |
| Chipotle  | 32   | 8218    |
| Mcdonald  | 7   | 24337   |
| Five Guys | 45   |6617    |
| Walmart   | 23   |10739    |
| Subway    | 5   |29509    |
| Olive Garden| 48   |5764    |
| PF Change | 109   |2370    |

They are all really bad

---

# Then look at some correlations:


#### First # of Review and rating

<div>
    <a href="https://plot.ly/~FrankQiu/135/" target="_blank" title="stars vs num_review" style="display: block; text-align: center;"><img src="https://plot.ly/~FrankQiu/135.png" alt="stars vs num_review" style="max-width: 100%;width: 600px;"  width="600" onerror="this.onerror=null;this.src='https://plot.ly/404.png';" /></a>
    <script data-plotly="FrankQiu:135"  src="https://plot.ly/embed.js" async></script>
</div>

maybe then group into bins:


<div>
    <a href="https://plot.ly/~FrankQiu/139/" target="_blank" title="ag_review_df$stars vs ag_review_df$review_round" style="display: block; text-align: center;"><img src="https://plot.ly/~FrankQiu/139.png" alt="ag_review_df$stars vs ag_review_df$review_round" style="max-width: 100%;width: 600px;"  width="600" onerror="this.onerror=null;this.src='https://plot.ly/404.png';" /></a>
    <script data-plotly="FrankQiu:139"  src="https://plot.ly/embed.js" async></script>
</div>


So not really corralted

#### Then price range and rating


<div>
    <a href="https://plot.ly/~FrankQiu/147/" target="_blank" title="ag_price_df[, 2] vs ag_price_df[, 1]" style="display: block; text-align: center;"><img src="https://plot.ly/~FrankQiu/147.png" alt="ag_price_df[, 2] vs ag_price_df[, 1]" style="max-width: 100%;width: 600px;"  width="600" onerror="this.onerror=null;this.src='https://plot.ly/404.png';" /></a>
    <script data-plotly="FrankQiu:147"  src="https://plot.ly/embed.js" async></script>
</div>


#### Not very corrlated

# Then other Interesting attributes:

## Ambience

|  Ambience   |      |
|-------------|------|
|   casual    |      |
|   classy    |      |
|   divey     |      |
|   hipster   |      |
|   intimate  |      |
|   romantic  |      |
|   touristy  |      |
|   trendy    |      |
|   upscale   |      |

<div>
    <a href="https://plot.ly/~FrankQiu/162/" target="_blank" title="ag_ambience_df[, 2] vs ag_ambience_df[, 1]" style="display: block; text-align: center;"><img src="https://plot.ly/~FrankQiu/162.png" alt="ag_ambience_df[, 2] vs ag_ambience_df[, 1]" style="max-width: 100%;width: 600px;"  width="600" onerror="this.onerror=null;this.src='https://plot.ly/404.png';" /></a>
    <script data-plotly="FrankQiu:162"  src="https://plot.ly/embed.js" async></script>
</div>


#### We can sort it 

<div>
    <a href="https://plot.ly/~FrankQiu/164/" target="_blank" title="ag_ambience_df_sort[, 2] vs ag_ambience_df_sort[, 1]" style="display: block; text-align: center;"><img src="https://plot.ly/~FrankQiu/164.png" alt="ag_ambience_df_sort[, 2] vs ag_ambience_df_sort[, 1]" style="max-width: 100%;width: 600px;"  width="600" onerror="this.onerror=null;this.src='https://plot.ly/404.png';" /></a>
    <script data-plotly="FrankQiu:164"  src="https://plot.ly/embed.js" async></script>
</div>

## Diet

|   Diet      |      |
|-------------|------|
|  dairy-free |      |
| gluten-free |      |
|    halal    |      |
|   kosher    |      |
|   soy-free  |      |
|   vegan     |      |
| vegetarian  |      |


<div>
    <a href="https://plot.ly/~FrankQiu/168/" target="_blank" title="ag_diet_df[, 2] vs ag_diet_df[, 1]" style="display: block; text-align: center;"><img src="https://plot.ly/~FrankQiu/168.png" alt="ag_diet_df[, 2] vs ag_diet_df[, 1]" style="max-width: 100%;width: 600px;"  width="600" onerror="this.onerror=null;this.src='https://plot.ly/404.png';" /></a>
    <script data-plotly="FrankQiu:168"  src="https://plot.ly/embed.js" async></script>
</div>


#### Then sort it


<div>
    <a href="https://plot.ly/~FrankQiu/170/" target="_blank" title="ag_diet_df_sort[, 2] vs ag_diet_df_sort[, 1]" style="display: block; text-align: center;"><img src="https://plot.ly/~FrankQiu/170.png" alt="ag_diet_df_sort[, 2] vs ag_diet_df_sort[, 1]" style="max-width: 100%;width: 600px;"  width="600" onerror="this.onerror=null;this.src='https://plot.ly/404.png';" /></a>
    <script data-plotly="FrankQiu:170"  src="https://plot.ly/embed.js" async></script>
</div>


## Background music

|    background    |      |
|------------------|------|
| background_music |      |
|        dj        |      |
|      jukebox     |      |
|       karaoke    |      |
|      live        |      |
|      playlist    |      |
|       video      |      |
|       noise      |      |


<div>
    <a href="https://plot.ly/~FrankQiu/154/" target="_blank" title="ag_background_df[, 2] vs ag_background_df[, 1]" style="display: block; text-align: center;"><img src="https://plot.ly/~FrankQiu/154.png" alt="ag_background_df[, 2] vs ag_background_df[, 1]" style="max-width: 100%;width: 600px;"  width="600" onerror="this.onerror=null;this.src='https://plot.ly/404.png';" /></a>
    <script data-plotly="FrankQiu:154"  src="https://plot.ly/embed.js" async></script>
</div>

#### we can also sort it 

<div>
    <a href="https://plot.ly/~FrankQiu/156/" target="_blank" title="ag_background_df_sort[, 2] vs ag_background_df_sort[, 1]" style="display: block; text-align: center;"><img src="https://plot.ly/~FrankQiu/156.png" alt="ag_background_df_sort[, 2] vs ag_background_df_sort[, 1]" style="max-width: 100%;width: 600px;"  width="600" onerror="this.onerror=null;this.src='https://plot.ly/404.png';" /></a>
    <script data-plotly="FrankQiu:156"  src="https://plot.ly/embed.js" async></script>
</div>



|    parking   |      |
|--------------|------|
|     garage   |      |
|     street   |      |
|     valet    |      |
|    validated |      |




|    feature   |      |
|--------------|------|
|   Delivery   |      |
| Dogs Allowed |      |
|  Drive-Thru  |      |
|  Happy Hour  |      |
|    Wi-Fi     |      |





|  highlights |      |
|-------------|------|
|   Dancing   |      |
|   kids      |      |
|   breakfast |      |
|   brunch    |      |
|   dessert   |      |
|   dinner    |      |
|   latenight |      |
|   lunch     |      |



# Neighbour

# later:

- Keep explore correlation
- Does the rating a reflection of sentiment in general?
- Use comparison between 




