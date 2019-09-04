[Think Stats Chapter 5 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2006.html#toc50) (blue men)

Given a normal distribution of heights in the united states, we compute the cdf using a normal distribution with the provided mean and standard deviation.  We take the upper range of the cdf, all heights below 6'1, and subtract all heights above 5'10 to get the probability range.

```python
import brfss
from scipy import stats
df = brfss.ReadBrfss()

mu = 178
sigma = 7.7
dist = stats.norm(loc=mu, scale=sigma)
lower = 70 * 2.54
upper = 73 * 2.54
pctg = dist.cdf(upper) - dist.cdf(lower)
print(pctg, pctg * df.shape[0])

0.34274683763147457 142071.6489197849
```

To test this model, we can plot a heights vs normal stdev line and compare the cdf of the actual data.  It is a close match to our fit line for the heights we are testing.

```python
heights = df.htm3

mean = heights.mean()
std = heights.std()

xs = [-4, 4]
fxs, fys = thinkstats2.FitLine(xs, inter=mean, slope=std)
thinkplot.Plot(fxs, fys, color='gray', label='model')

xs, ys = thinkstats2.NormalProbability(df.htm3)
thinkplot.Plot(xs, ys, label='Heights')
```
