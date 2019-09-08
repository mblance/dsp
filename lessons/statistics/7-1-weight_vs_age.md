[Think Stats Chapter 7 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2008.html#toc70) (weight vs. age)

We extract the age and birthweight from the live birth dataset.  Age vs weight is plotted, with outliers trimmed on the axis.  Mothers under the age of 14 are extreme outliers, as are birth weights under 2 lbs and over 14 lbs. We set an alpha=0.12 so we can more accurately see the spread of the data, which is helping some.

```python
age, birthweight = live['agepreg'], live['totalwgt_lb']

thinkplot.Scatter(age, birthweight, alpha=0.12)
thinkplot.Config(xlabel='Mothers Age',
                 ylabel='Birth Weight (lbs)',
                 axis=[14, 40, 2, 13],
                 legend=False)
```

We calculate spearman's and pearsons from the data, seeing that there is a positive weak correlation.  Our spearman algorithm is ranking rather than based on the value of the x,y pairs, which has a normalizing effect on outliers.  Because of the large number of outliers, our spearman's value is higher than pearsons.

```python
age.corr(birthweight, method='spearman'), age.corr(birthweight, method='pearson')
(0.09461004109658226, 0.0688339703541091)
```

Our data visualization here has limitations, we can't fully grasp the spread of the data.  By categorizing age into bins and calculating the mean of the bin, then plotting that vs the percentiles from the cdf of the birth weight, we can see where most of our data is concentrated.  Taking both graphs together, as we approach age 40 the quantity of data decreases and the number of outliers increases.  For further experimentation, we can view data in only the bulk of the dataset (women under 35 or so) and see if the quality of our correlation is better, IE with fewer outliers.

```python
bins = np.arange(15, 41, 5)
indices = np.digitize(age, bins)
groups = live.groupby(indices)

mean_heights = [group.agepreg.mean() for i, group in groups]
cdfs = [thinkstats2.Cdf(group.totalwgt_lb) for i, group in groups]

for percent in [75, 50, 25]:
    weight_percentiles = [cdf.Percentile(percent) for cdf in cdfs]
    label = '%dth' % percent
    thinkplot.Plot(mean_heights, weight_percentiles, label=label)
    
thinkplot.Config(xlabel='Mothers Age',
                 ylabel='Weight',
                 axis=[14, 40, 2, 13],
                 legend=True)
```
