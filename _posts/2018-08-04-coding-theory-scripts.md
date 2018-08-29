---
layout: post
title:  Coding Theory Scripts
image: ''
date:   2018-08-04 20:1:42
tags:
- coding theory
description: ‘’
categories:
- Coding
---
Here are some coding theory scripts I’ve written in python for ease of learning and to handle homework tasks from the Hankerson textbook.

## KBITS
KBITS FUNCTION for generating all binary numbers of length n and k 1 bits.

{% highlight python %}
	import itertools
	def kbits(n, k):
	    result = \[]
	    for bits in itertools.combinations(range(n), k):
	s = \['0'] \* n
	for bit in bits:
	s\[bit] = '1'
	result.append(''.join(s))
	return result
{% endhighlight %}

## Likelihood
LIKE FUNCTION for finding out probability that if v is sent, w is received.
**input**: word sent, word received, probability of error
**output**: probability that the word w is received
{% highlight python %}
def like(v,w,p):
exp = len(v)
if v == w is True:
print('same same haha youre lame')
else:
summ = sum(x!=y for x,y in zip(v,w))
probs = p\**(exp - summ) * (1-p)\*\*(summ)
return round(probs, 10)
{% endhighlight %}

## Most Likely Word Send
BEST FUNCTION for finding out best w for given V"

**input format:** word received, all elements of C as individual string arguments

**output**: best possible value of v
{% highlight python %}
	def best(w,*args):
	    sume = sum(len(str(x)) for x in args)
	    listie = list()
	    for x in args:
	        summ = sum(a!=b for a,b in zip(w,x))
	        listie.append(summ)
	    dictie = dict(zip(args,listie))
	    for i in dictie:
	        if dictie[i]  == min(dictie[i] for i in dictie):
	            closest = i
	    return dictie
{% endhighlight %}

## Error Pattern
EP FUNCTION for finding out error pattern

**input format**: word received, all elements of C as individual string arguments

**output**: all error patterns of w
{% highlight python %}
	def ep(w,*args):
	    listie = list()
	    for x in args:
	        thing = int(w,2) ^ int(x,2)
	        news = '{0:0{1}b}'.format(thing,len(w))
	        listie.append(news)
	    dictie = dict(zip(args,listie))
	    return listie
{% endhighlight %}

## Incomplete Maximum Likelihood Decoder
IMLD FUNCTION for finding out the best fit v for a given w through xor'ing through all the possible words in C
**input format**: word received, all elements of C as individual string arguments
**output**: error patterns of w, closest v value, dictionary of word in C : weight of error pattern for reference
{% highlight python %}
	def imld(w, *args):
	    eplist = list()
	    listie = list()
	    for x in args:
	        thing = int(w,2) ^ int(x,2)
	        news = '{0:0{1}b}'.format(thing,len(w))
	        eplist.append(news)
	        summ = sum(a!=b for a,b in zip(w,x))
	        listie.append(summ)
	    dictie = dict(zip(args,listie))
	    for i in dictie:
	        if dictie[i]  == min(dictie[i] for i in dictie):
	            closest = i
	    return ' '.join(eplist), closest, dictie
{% endhighlight %}

## Reliability of MLD
REL FUNCTION for finding out probability theta p as sum of probability of v = w
**input format**: word sent, probability of error, set L(v)
**output**: theta p
ENTER P AS NUMBER NOT STRING!"""
{% highlight python %}
	def rel(v,p,*args):
	    exp = len(v)
	    theta = 0
	    listie = list()
	    for w in args:
	        if v == w is True:
	            print('same same haha youre lame')
	        else:
	            summ = sum(x!=y for x,y in zip(v,w))
	            probs = p**(exp-summ) * (1-p)**(summ)
	            listie.append(probs)
	            theta += probs
	    return theta
{% endhighlight %}

## Correctable Error Patterns
ERR FUNCTION for finding out all error patterns that will be corrected
**input format**:setC containing, all error patterns,
**output**: list of correctable things
{% highlight python %}
	def err(a,b,*args):
	    patterns = list()
	    argu = list(args)
	    for x in args:
	        thing = int(a,2) ^ int(x,2)
	        tidy = '{0:0{1}b}'.format(thing,len(a))
	        distancea = sum(x!=y for x,y in zip(a,tidy))
	        distanceb = sum(x!=y for x,y in zip(b,tidy))
	        if distancea < distanceb:
	            patterns.append(tidy)
	    return patterns
{% endhighlight %}