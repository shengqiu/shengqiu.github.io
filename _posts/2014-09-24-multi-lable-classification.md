---
layout: post
title:  "ML Class"
date:   2014-09-24 14:22:19
categories: yelp_project
---

## Theories

---

# **Generative Models**

– Needs P(features|class)

– **Gaussian discriminant analysis (GDA)**:Assume that p(xi | yi) follows a multivariate normal distribution.

– **Naive Bayes (NB)**: Assume that variables in xi are independent of each other given yi.

---

# **parametric methods**

- There are a fixed number of “parameters” in the model (e.g., number of rules).
- As you get more data, you can estimate them more accurately.
- But at some point, more data doesn’t help because model is too simple. E.g., depth-3 decision trees can’t model most distributions.

---

# **Non-parametricmodels**

– Number of parameters grows with the number of training examples
- Model gets more complicated as you get more data.

---

# **Boosting**: uses classifiers that
– Can obtain >50% accuracy on weighted training data.
– is simple

Basic steps:

1. Fit a classifier on the training data.
2. Give a higher weight to examples that the classifier got wrong.
3. Fit a classifier on the weighted training data.
4. Go back to 2.

# **Averaging**: 

use different models and go for the most vote.


# **Bootstrap sample**: 

chosen independently from list with replacement.

---

# **Precision** = TP/(TP + FP)

High precision means the filtered messages are likely to really be spam.

# **Recall** = TP/(TP + FN)

High recall means that most spam messages are filtered.


---

# Basics

$$(\boldsymbol{A}\boldsymbol{B})^{-1}=\boldsymbol{B}^{-1}\boldsymbol{A}^{-1}$$

$$(\boldsymbol{A}^{T})^{-1}=(\boldsymbol{A}^{-1})^{T}$$

$$(\boldsymbol{A}+\boldsymbol{B})^{T}=\boldsymbol{A}^{T}+\boldsymbol{B}^{T}$$

$$(\boldsymbol{A}\boldsymbol{B})^{T}=\boldsymbol{B}^{T}\boldsymbol{A}^{T}$$

$$(\boldsymbol{A}\boldsymbol{B})^{2}=\boldsymbol{A}\boldsymbol{B}\boldsymbol{A}\boldsymbol{B}$$

---

# Derivatives

$$\partial {(\alpha{\boldsymbol{X}})} = \alpha (\partial{\boldsymbol{X}})$$

$$\partial {(\boldsymbol{X} + \boldsymbol{Y})} = (\partial \boldsymbol{X} + \partial \boldsymbol{Y})$$

$$\partial {(\boldsymbol{X} \boldsymbol{Y})} = (\partial \boldsymbol{X})\boldsymbol{Y} +  \boldsymbol{X} (\partial \boldsymbol{Y})$$

$$\partial {\boldsymbol{X}} ^ {T}=  (\alpha \boldsymbol{X})^{T}$$

$$ \frac{\partial{a^{T}\boldsymbol{X}b}} {\partial \boldsymbol{X}} =ab^T $$

$$ \frac{\partial{a^{T}{\boldsymbol{X}}^{T}b}} {\partial \boldsymbol{X}} =ba^T  $$

---

# Derivatives of an Inverse

$$\frac{\partial {\boldsymbol{Y} ^{-1}}}{\partial{x}} = -\boldsymbol{Y} ^{-1}\frac{\partial {\boldsymbol{Y}} } {\partial{x}} {\boldsymbol{Y} ^{-1}}$$

$$\frac{a^{T}\partial {\boldsymbol{X} ^{-1}}b} {\partial{\boldsymbol{X}}} = -\boldsymbol{X} ^{-T}ab^{T}{\boldsymbol{X} ^{-T}}$$

---

## Decision Stump

**pseudo code**

1. compute accuracy for each based on each value of the features in data
2. choose the best rule with the best cut line

**cost**

- there are d features
- Sort the examples for each feature, cost O(nlogn), and update score cost O(n), so O(nlogn) + o(n) = O(nlogn)
- so the total is O(dnlogn)

* cost of decision tree is O(NDM)

---

## KNN

**pseudo code**

1. D = X.^2*ones(D,T) + ones(N,D)*(Xtest’).^2 - 2*X*Xtest’
2. Sort D for each Xtest data point
3. get the major vote.

**cost**

1. Use Quick sort to find the kth element, which costs O(n)
2. go through all X data points and find all of those that are smaller that the kth, which cost O(n)
3. the total cost is O(n) + O(n) = O(n)


---

## Naive Bayes

**pseudo code**

{% highlight matlab %}
p_xy = zeros(D, 2, C);
for c = 1:C
	for j = 1:D
		p_xy(j,1,c) = sum(X(y==c,j)==1)/counts(c);
		p_xy(j,1,c) = sum(X(y==c,j)==0)/counts(c);
	end
end
{% endhighlight %}

**cost**

For each of the T examples, the dominant cost is computing P(x_ij|y_i) 

for all D values of j and yi. You can do this with three ‘’for’ loops (as in the naive Bayes predict function in the given code), giving a total time of O(TDC) if you have C classes (we’ll accept answers that ignore the dependence on C, although in practice this is important if C is large). 


---

## Random forests 

Averaging a set of deep decision trees

**pseudo code**

1. **Bootstrap**: sample n elements with replacement.

**cost**

- If the number of features is large, better training error, but a bad approximation of the testing error
- If the number of trees is large, bigger training error, but it is a good approximation of the testing error.

---

## Kmeans

**pseudo code**

1. Start with ‘k’ initial ‘means’
2. Assign each object to the closest mean.
3. Update the mean of each group.
4. Assign each object to the closest mean.
5. Repeat and stop if no objects change groups.

---

## Kmeans++

**pseudo code**

1. initialize the first cluster
2. Compute distance x_i to each mean μ_c.
	d = ||x_i - μ_c||
3. For each object set di to the minimum distance across all clusters c.
	d = min {d_ic}
4. Choose next mean by sampling proportional to (d_i)^2
	p_i = d^2/sum(d^2)
5. Stop when we have k means, otherwise return to 2.

{% highlight matlab %}
for k = 2:K
	D = X.^2*ones(D,k-1) + ones(N,D)*(means').^2 - 2*X*means';
	minD = min(distances,[],2);
	i = samplediscrete()
{% endhighlight %}

---

## DBSCAN

**parameter**

– Radius: minimum distance between points to be considered ‘close’.
– MinPoints: number of ‘close’ points needed to define a cluster.

**pseudo code**

– For each example xi:

If xi is already assigned to a cluster, do nothing.

If xi is not core point (less than minPoints neighbours with distance ≤ ‘r’), do nothing.

If xi is a core point, expand cluster.

– Expand cluster function:

Assign all xj within distance ‘r’ of core point xi to cluster.

For each newly-assigned neighbour xj that is a core point, expand cluster.

**cost**

1. distance between all pairs of objects. 

– Cost of computing distance with ‘d’ features is O(d).
– There are O(n2) pairs of objects.
– So cost of computing all pairs of distances is O(n2d).

2. Given the distances, total cost of all expand operations is O(n2).

## UBClustering



## Amazon

– Only consider rules (S => T) where S and T have a size of 1
– Only consider sets S and T that have previously been bought together
– For each item, construct ‘bag of users’ vector xi
– Recommend items with highest cosine similarity




<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>





