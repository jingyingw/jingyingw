---
layout: post
title:  Number Theory Scripts
image: ''
date:   2018-08-05 23:31:50
tags:
- crypto
- math
description: ‘’
categories:
- Cryptology
---
Here are some python scripts relating to primes.
## Greatest Common Denominator
This is a script that calculates the GCD of two integers using the Euclidean algorithm.

{% highlight python %} 
	def gcd(a,b):
	    while b%a != 0:
	        remainder = b % a
	        b = a
	        a = remainder
	    else:
	        return a
{% endhighlight %}

## Extended Euclidean Algorithm
The EEA computes for you the GCD of two numbers _a,b_ written as a sum of their respective multiples.

It also returns the multiplicative inverse a^-1 of b.

{% highlight python %} 
	def ext(a,b):
	    originala = a
	    originalb = b
	    x1 = 0
	    x2 = 1
	    y1 = 1
	    y2 = 0
	    while b%a != 0:
	        remainder = b % a
	        q = (b-remainder)/a
	        b = a
	        a = remainder
	        newx = (-q*x2)+x1
	        x1 = x2
	        x2 = newx
	        newy = (-q*y2)+y1
	        y1 = y2
	        y2 = newy
	    else:
	        print(originala,"*",newx,'+',originalb,'*',newy,'=',originala*newx+originalb*newy)
	    return newx
{% endhighlight %}
## Congruence Unknown Solver
This script solves for x in the equation ax ≡ c mod n. Note that it depends upon the outputs of my GCD and EEA scripts.

If a is coprime to n, then no issue. It’s fast because you just EEA and find x through multiplication of c with the result. If a is *not* coprime to n, then some issue appears that are solved by using the GCD of a and n. A list of solutions for x will be returned. 

**Input**: As listed in the equation above, a,c,n in exact positions

**Output**: Value(s) for x

{% highlight python %} 
	def solve(a,c,n):
	    if gcd(a,n) == 1:
	        newx = ext(a,n)
	        return c*newx % n
	    if gcd(a,n) > 1:
	        listie = list()
	        d = gcd(a,n)
	        if c  %gcd(a,n)!= 0:
	            return 'no solution'
	        else:
	            newx = ext((a/d),(n/d))
	            x0 = (c/d)*newx % (n/d)
	            var = 0
	            while var <= (d-1):
	                listie.append((x0+var*(n/d)) % n)
	                var = var +1
	            else:
	                return listie
{% endhighlight %}
## Factoring
This is a stupid stupid method that lists all factors of a number. It literally checks all the numbers smaller than itself. Mainly for my convenience.

If it’s prime, the script says it’s prime, with a exclamation mark like this!
{% highlight python %} 
	def fact(a):
	    var = 1
	    listie = [0]
	    while a not in listie:
	            if a % var == 0:
	                listie.append(var)
	                var = var+1
	            else:
	                var = var+1
	    else:
	        if len(listie)==3:
	            print("Prime!")
	            return 0
	        else:
	            del listie[0]
	            return listie
{% endhighlight %}
## Chinese Remainder Theorem
This script finds a ≡ x mod mn from inputs a mod m and b mod n, using the CRT.

**Input**: As listed in the equation above, a,c,n in exact positions

**Output**: Value for x

{% highlight python %} 
	def cong(a,m,b,n):
	    inv = ext(n,m)
	    c = ((a-b)*inv) % m
	    k = b+n*c
	    print(a,"≡",k,"mod",n*m)
	    return k
{% endhighlight %}
## Solving 2 Congruences - Does not work!
This doesn’t seem to work but it tries to solve input: x^2 ≡ 1 mod n if you know how to make it work lmn
{% highlight python %} 
	def sqs(n):
	    list1 = fact(n)
	    final = list()
	    del list1[0:2]
	    del list1[-1]
	    for x in list1:
	        variable = 1
	        k = cong(1,x,-1,list1[-variable])
	        j = cong(-1,x,-1,list1[-variable])
	        y = cong(1,x,1,list1[-variable])
	        l = cong(-1,x,-1,list1[-variable])
	        final.append(k)
	        variable += 1
	    return list1
{% endhighlight %}
## Modular Exponentiation of 2^n mod k.
This script computes 2^n mod k somewhat intelligently using congruences. That’s it.
{% highlight python %} 
	def exp(n,k):
	    first = list(reversed(list('{0:b}'.format(n))))
	    listie = list()
	    mods = list()
	    variable = 0
	    for x in first:
	        listie.append(int(x)*(2**variable))
	        variable = variable + 1
	    listie[:] = (value for value in listie if value != 0)
	    for y in listie:
	        mods.append((2**y)%k)
	    number = reduce(lambda x, y: x*y, mods)
	    return number
{% endhighlight %}
## Euler’s Function
This does the Euler’s Function, which finds how many integers there are that are coprime to your number but smaller than your number.
{% highlight python %} 
	def phi(n):
	    listie = fact(n)
	    phi = [1, ]
	    del listie[-1]
	    for x in range(1,n):
	        if gcd(x,n)==1 and x not in listie:
	            phi.append(x)
	    return len(phi)
{% endhighlight %}