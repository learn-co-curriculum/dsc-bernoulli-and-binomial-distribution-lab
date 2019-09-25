
# Bernoulli and Binomial Distribution - Lab

## Introduction
In this lab, you'll practice your newly gained knowledge on the Bernoulli and Binomial Distribution.

## Objectives
You will be able to:
* Apply the formulas for the Binomial and Bernoulli distributions
* Apply NumPy to randomly generate Binomial and Bernoulli trials
* Use Matplotlib to generate Binomial and Bernoulli trials with various probabilities

## Apply the formulas for the Binomial and Bernoulli distributions

When playing a game of bowling, what is the probability of throwing exactly 3 strikes in a game with 10 rounds? Assume that the probability of throwing a strike is 25% for each round. Use the formula for the Binomial distribution to get to the answer. You've created this before, so we provide you with the function for factorials again:


```python
def factorial(n):
    prod = 1
    while n >= 1:
        prod = prod * n
        n = n - 1
    return prod
```


```python
p_3_strikes = None #answer = 0.2502822
```




    0.25028228759765625




```python
# __SOLUTION__ 
def factorial(n):
    prod = 1
    while n >= 1:
        prod = prod * n
        n = n - 1
    return prod
```


```python
# __SOLUTION__ 
p_3_strikes = (factorial(10)/(factorial(7)*factorial(3)))*(0.25)**3*(0.75)**7
p_3_strikes
```




    0.25028228759765625



Now, create a function for the Binomial distribution with three arguments $n$, $p$ and $k$ just like in the formula:

$$ \large P(Y=k)= \binom{n}{k} p^k(1-p)^{(n-k)}$$ 



```python
def binom_distr(n,p,k):
    None
```


```python
# __SOLUTION__ 
def binom_distr(n,p,k):
    p_k = (factorial(n)/(factorial(k)*factorial(n-k)))*(p**k*(1-p)**(n-k))
    return p_k
```

Validate your previous result by applying your new function.


```python
# Your code here
```




    0.25028228759765625




```python
# __SOLUTION__ 
binom_distr(10,0.25,3)
```




    0.25028228759765625



Now write a `for` loop along with your function to compute the probability that you have five strikes or more in one game. You'll want to use `numpy` here!


```python
import numpy as np
# Your code here
```


```python
# __SOLUTION__ 
import numpy as np
prob = 0
for i in np.arange(5,11):
     prob += binom_distr(10,0.25,i)
```

## Use a simulation to get the probabilities for all the potential outcomes

Repeat the experiment 5000 times.


```python
# leave the random seed here 
np.random.seed(123)
#
#
#
#
```


```python
# the results should look like this:
# [0 1 2 3 4 5 6 7 8]
# [ 310  941 1368 1286  707  297   78   11    2]
```

    [0 1 2 3 4 5 6 7 8]
    [ 258  922 1475 1264  706  272   86   13    4]



```python
# __SOLUTION__ 
np.random.seed(243)
n = 5000
iteration = []
for loop in range(n):
    iteration.append(np.random.binomial(10, 0.25))
    np_it = np.array(iteration)
```


```python
# __SOLUTION__ 
values, counts = np.unique(np_it, return_counts=True)
print(values)
print(counts)
```

    [0 1 2 3 4 5 6 7 8]
    [ 258  922 1475 1264  706  272   86   13    4]


## Visualize these results

Create the PMF using these empirical results (that is, the proportions based on the values we obtained running the experiment 5000 times).


```python
import matplotlib.pyplot as plt
#
#
#
#
```


![png](index_files/index_20_0.png)



```python
# __SOLUTION__ 
import matplotlib.pyplot as plt
plt.bar(values, counts/5000, align='center', alpha=0.8)
plt.xticks(values)
plt.ylabel('Fraction')
plt.title('PMF of strikes in a bowling game');
```


![png](index_files/index_21_0.png)


You can see that, with a 25% strike hit rate, even when simulating 5000 times, an almost perfect and/or perfect game of 9 and 10 strikes didn't even occur once! If you change your seed, however, you'll see that perfect games will show up occasionally. 

Next, let's create the CDF based on these results. You can use `np.cumsum` to obtain cumulative probabilities.


```python
# Your code here
#
#
#
#
```


![png](index_files/index_23_0.png)



```python
# __SOLUTION__ 
import matplotlib.pyplot as plt
plt.bar(values, np.cumsum(counts/5000), align='center', alpha=0.8)
plt.xticks(values)
plt.ylabel('Fraction')
plt.title('CDF of strikes in a bowling game');
```


![png](index_files/index_24_0.png)


## Summary

Congratulations! In this lab, you practiced your newly gained knowledge of the Bernoulli and Binomial Distribution.
