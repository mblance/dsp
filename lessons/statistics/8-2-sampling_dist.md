[Think Stats Chapter 8 Exercise 2](http://greenteapress.com/thinkstats2/html/thinkstats2009.html#toc77) (scoring)

We get our xbars by running Estimate3 with n=10.  Each of the xs (samples of x) are pulled from the exponential distribution and means are calculated with L = 1 / lambda.  Our RMSE is calculated from L.

```python
def Estimate3(n=7, iters=1000):
    lam = 2

    means = []
    medians = []
    for _ in range(iters):
        xs = np.random.exponential(1.0/lam, n)
        L = 1 / np.mean(xs)
        Lm = np.log(2) / thinkstats2.Median(xs)
        means.append(L)
        medians.append(Lm)

    print('rmse L', RMSE(means, lam))
    return means
    
xbars = Estimate3(n=10, iters=1000)
rmse L 0.7919077526202096
```
We take our xbars returned from our estimate function and plot the CDF, the means appear to be normally distributed with a right skew and the average of the sample means is about 2.229 at n=10 with a confidence interval of 1.292 - 3.6028

```python

cdf = thinkstats2.Cdf(xbars)
print(np.mean(xbars))
thinkplot.Cdf(cdf)
thinkplot.Config(xlabel='Sample mean',
                 ylabel='CDF')

confidence = (cdf.Percentile(5), cdf.Percentile(95))
print(confidence)

2.228701866246173
(1.2924731308057844, 3.602874757065167)
```

Using a small n gets us a large number of random samples that are mostly outliers.  Increasing n has the effect of reducing this outlier selection effect and giving us a better mean with a distribution that is less skewed and a tighter confidencce interval.  This new value is closer to the lambda and is a predicted lambda value.

```python

xbars = Estimate3(n=20, iters=1000)
rmse L 0.7919077526202096

cdf = thinkstats2.Cdf(xbars)
print(np.mean(xbars))
thinkplot.Cdf(cdf)
thinkplot.Config(xlabel='Sample mean',
                 ylabel='CDF')

confidence = (cdf.Percentile(5), cdf.Percentile(95))
print(confidence)

2.1139625351888833
(1.468733496594947, 3.0171281927689324)
```

