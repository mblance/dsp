[Think Stats Chapter 6 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2007.html#toc60) (household income)

Functions are provided in notebook chap06ex.ipynb

We read the income data and get the income sample.  The sample is truncated to show earners at or below 1 million dollars per year.  We take the median, mean, and skewness of the sample, which shows that income is heavily right skewed with a mean that is well over the median.  This indicates that most people make below the mean income.

```python
import hinc
income_df = hinc.ReadData()
log_sample = InterpolateSample(income_df, log_upper=6.0)
sample = np.power(10, log_sample)

Median(sample), sample.mean(), PearsonMedianSkewness(sample)

(51226.45447894046, 74278.7075311872, 0.7361258019141795)
```

In fact if we plot the cdf this seems to give a pretty clear picture of where the wealth is concentrated, showing that people in the bottom 50% of earners have a much smaller share of the wealth.

```python
cdf = thinkstats2.Cdf(sample)
thinkplot.Cdf(cdf)
thinkplot.Config(xlabel='Household income ($)',
               ylabel='CDF')
```

If we take the cdf probability at the mean data point, we get the percentile of earners who make the mean or less.  This shows that a large majority of earners are below the mean.

```python
cdf.Prob(sample.mean())
0.660005879566872
```

If we cut off the earners at 10 million (log10 x == 7) and re run our numbers we get an even larger skew effect, with the median staying the same and the mean skyrocketing.  We see that 85% of the earners are now below the mean.

```python
Median(sample), sample.mean(), PearsonMedianSkewness(sample)
(51226.45447894046, 124267.39722164703, 0.39156450927742104)

cdf.Prob(sample.mean())
0.8565630665207663
```
