---
layout: post
title:  "Try Pymongo"
date:   2001-01-01 14:22:19
categories: pymongo
---

---
# build mongoDB

{% highlight r %}
cd dropbox/580_yelp/json
mongoimport --host=127.0.0.1 --db yelp --collection businesses yelp_academic_dataset_business.json
mongoimport --host=127.0.0.1 --db yelp --collection reviews yelp_academic_dataset_review.json
mongoimport --host=127.0.0.1 --db yelp --collection tips yelp_academic_dataset_tip.json
mongoimport --host=127.0.0.1 --db yelp --collection users yelp_academic_dataset_user.json
mongoimport --host=127.0.0.1 --db yelp --collection checkins yelp_academic_dataset_checkin.json
{% endhighlight %}

---
# Connect to MongoDB

1. conenct to MongoDB
2. connect to a database
3. connect to a collection (table)

{% highlight python%}
from pymongo import MongoClient

client = MongoClient('localhost', 27017)
db = client.test_db
collection = db.test_collection
{% endhighlight %}

---

# Insert a Document

1. create a document using dictionary in python
2. insert to a collection using insert() method

{% highlight python%}
import datetime
post = {	"author": "Mike",
"text": "My first blog post!",
"date": datetime.datetime.utcnow()}
{% endhighlight %}

---
# Update Documents






# Some Query

1. Every document in the collection
2. Every document meet the criteria
3. One of the documents meet the criteria
4. Every document meet the criteria, sorted descending
5. Count number of documents that meet the criteria

{% highlight python%}
collection.find()
collection.find({'review_count': {'$let': 3}})
collection.find_one({'review_count': {'$let': 3}})
collection.find({'review_count': {'$let': 3}}).sort('review_count': -1)
collection.find({'review_count': {'$let': 3}}).count()
{% endhighlight %}

---

# Aggregation in mongoDB

**1. project operation**

{% highlight python%}
db.books.aggregate( 
		[ { $project : { title : 1 , author : 1 } } ] 
);
{% endhighlight %}
Passes along the documents with only the specified fields to the next stage in the pipeline. 


**2. match operation**

{% highlight python%}
db.articles.aggregate(
    [ { $match : { author : "dave" } } ]
);
{% endhighlight %}
Filters the documents to pass only the documents that match the specified condition(s) to the next pipeline stage.

**3. limit operation**

{% highlight python%}
db.article.aggregate(
    { $limit : 5 }
);
{% endhighlight %}
Limits the number of documents passed to the next stage in the pipeline.

**4. skip operation**

{% highlight python%}
db.article.aggregate(
    { $skip : 5 }
);
{% endhighlight %}
Skips over the specified number of documents that pass into the stage and passes the remaining documents to the next stage in the pipeline.

**5. unwind operation**

{% highlight python%}
{ "_id" : 1, "item" : "ABC1", sizes: [ "S", "M", "L"] }

db.inventory.aggregate( [ { $unwind : "$sizes" } ] )
{% endhighlight %}
Deconstructs an array field from the input documents to output a document for each element. Each output document is the input document with the value of the array field replaced by the element.

**6. group operation**

Deconstructs an array field from the input documents to output a document for each element. Each output document is the input document with the value of the array field replaced by the element.

{% highlight python%}
{ "_id" : 1, "item" : "ABC1", sizes: [ "S", "M", "L"] }
{ "_id" : 1, "item" : "abc", "price" : 10, "quantity" : 2, "date" : ISODate("2014-03-01T08:00:00Z") }
{ "_id" : 2, "item" : "jkl", "price" : 20, "quantity" : 1, "date" : ISODate("2014-03-01T09:00:00Z") }
{ "_id" : 3, "item" : "xyz", "price" : 5, "quantity" : 10, "date" : ISODate("2014-03-15T09:00:00Z") }
{ "_id" : 4, "item" : "xyz", "price" : 5, "quantity" : 20, "date" : ISODate("2014-04-04T11:21:39.736Z") }
{ "_id" : 5, "item" : "abc", "price" : 10, "quantity" : 10, "date" : ISODate("2014-04-04T21:23:13.331Z") }

db.sales.aggregate(
   [
      {
        $group : {
           _id : { month: { $month: "$date" }, day: { $dayOfMonth: "$date" }, year: { $year: "$date" } },
           totalPrice: { $sum: { $multiply: [ "$price", "$quantity" ] } },
           averageQuantity: { $avg: "$quantity" },
           count: { $sum: 1 }
        }
      }
   ]
)
{% endhighlight %}

The previous aggregation operation uses the `$group` stage to group the documents by the month, day, and year and calculates the total price and the average quantity as well as counts the documents per each group.

The operation returns the following results:

{% highlight python%}
{ "_id" : { "month" : 3, "day" : 15, "year" : 2014 }, "totalPrice" : 50, "averageQuantity" : 10, "count" : 1 }
{ "_id" : { "month" : 4, "day" : 4, "year" : 2014 }, "totalPrice" : 200, "averageQuantity" : 15, "count" : 2 }
{ "_id" : { "month" : 3, "day" : 1, "year" : 2014 }, "totalPrice" : 40, "averageQuantity" : 1.5, "count" : 2 }
{% endhighlight %}

| Name of operators| Description                                                                                                             |
|-------------|-------------------------------------------------------------------------------------------------------------------------|
| `$sum`      | Returns a sum for each group (Ignores non-numeric values).                                                              |
| `$avg`      | Returns an average for each group (Ignores non-numeric values).                                                         |
| `$first`    | Returns a value from the first document for each group (Order is only defined if the documents are in a defined order). |
| `$last`     | Returns a value from the last document for each group. Order is only defined if the documents are in a defined order.   |
| `$max`      | Returns the highest expression value for each group                                                                     |
| `$min`      | Returns the lowest expression value for each group.                                                                     |
| `$push`     | Returns an array of expression values for each group.                                                                   |
| `$addToSet` | Returns an array of unique expression values for each group. Order of the array elements is undefined.                  |

**7. Group by null**

The following aggregation operation specifies a group _id of null, calculating the total price and the average quantity as well as counts for all documents in the collection:

{% highlight python%}
db.sales.aggregate(
   [
      {
        $group : {
           _id : null,
           totalPrice: { $sum: { $multiply: [ "$price", "$quantity" ] } },
           averageQuantity: { $avg: "$quantity" },
           count: { $sum: 1 }
        }
      }
   ]
)
{% endhighlight %}

The operation returns the following result:

{% highlight python%}
{ "_id" : null, "totalPrice" : 290, "averageQuantity" : 8.6, "count" : 5 }
{% endhighlight %}

**7. Sort**

 - ascending : 1 
 - descending : -1

{% highlight python%}
db.users.aggregate(
   [
     { $sort : { age : -1, posts: 1 } }
   ]
)
{% endhighlight %}

**8. geoNear**


{% highlight python%}
db.places.aggregate([
   {
     $geoNear: {
        near: { type: "Point", coordinates: [ -73.99279 , 40.719296 ] },
        distanceField: "dist.calculated",
        maxDistance: 2,
        query: { type: "public" },
        includeLocs: "dist.location",
        num: 5,
        spherical: true
     }
   }
])
{% endhighlight %}



# Aggregation in Pymongo

**1. Framwork**

- Import the data

{% highlight python%}
from pymongo import MongoClient
db = MongoClient().aggregation_example
result = db.things.insert_many([{"x": 1, "tags": ["dog", "cat"]},
   {"x": 2, "tags": ["cat"]},
   {"x": 2, "tags": ["mouse", "cat", "dog"]},
   {"x": 3, "tags": []}])
result.inserted_ids
{% endhighlight %}	
	
	
- the pipeline	

{% highlight python%}	
from bson.son import SON
pipeline = [
   {"$unwind": "$tags"},
   {"$group": {"_id": "$tags", "count": {"$sum": 1}}},
   {"$sort": SON([("count", -1), ("_id", -1)])}
   ]
list(db.things.aggregate(pipeline))   
{% endhighlight %}