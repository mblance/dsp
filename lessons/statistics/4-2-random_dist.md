[Think Stats Chapter 4 Exercise 2](http://greenteapress.com/thinkstats2/html/thinkstats2005.html#toc41) (a random distribution)

We generate 1000 random numbers between 0.0 and 1.0 and plot them with thinkplot.Pmf.  We can see that the probability of any random number pmf(x) should approach 1 / 1000.  If we look at the plot, the distribution approaches uniform and appears to be square.  If we increase the sample size to 10000, we have a more perfect square.

```python
import numpy as np
import thinkstats2, thinkplot
pmf = thinkstats2.Pmf(np.random.random(1000))
thinkplot.Pmf(pmf)
```

Using the cdf we can see a line that is alomst perfectly diagonal.  This indicates that the sum of probabilities are uniformly increasing as we increment x.

```python
cdf = thinkstats2.Cdf(rand)
thinkplot.Cdf(cdf)
```
