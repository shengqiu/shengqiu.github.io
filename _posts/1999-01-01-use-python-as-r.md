---
layout: post
title:  "Use Python as I am using R"
date:   1999-01-01 00:00:00
categories: python2r
---

---
	
# First package is pandas


1. load data from csv

The chunksize parameter defines how many lines in total




```python
df = pd.read_csv('test.csv', chunksize=10000)
```

2. Since you are using pandas already, use more `apply` and `map`

