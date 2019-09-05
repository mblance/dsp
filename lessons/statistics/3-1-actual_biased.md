[Think Stats Chapter 3 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2004.html#toc31) (actual vs. biased)

The probabilty mass function allows us to track the probability of each event in our sample.  Actual data deals with hard facts, biased data deals with people's reports of their own observations.  For children's perceptions of their family size, we can expect them to overreport the number of members of their family

We compute the pmf with thinkstats2.  This should always be the frequency of each data point divided by the sample size.  Then, we bias the data.

```python
import thinkstats2
import nsfg

resp = nsfg.ReadFemResp()
pmf = thinkstats2.Pmf(resp['numkdhh'])
biased_pmf = BiasPmf(pmf, label='Biased Family Size')
```


Our BiasPmf function takes the actual data's family size (x), looks up the probability of that size, and multiplies it by x.  These new probabilities are then normalized by dividing by the sample size n.

```python
def BiasPmf(pmf, label):
    new_pmf = pmf.Copy(label=label)

    for x, p in pmf.Items():
        new_pmf.Mult(x, x)
        
    new_pmf.Normalize()
    return new_pmf
```
We plot the pmf vs the biased pmf.  At zero we expect the bias to be zero, everywhere else we can see that applying this scaling will will skew the family size higher.

```python
import thinkplot
thinkplot.PrePlot(2)
thinkplot.Pmfs([pmf, biased_pmf])
thinkplot.Config(xlabel='Family Size', ylabel='PMF')
```

We can then compute the mean of the actual pmf by summing the product of the family size x with the probability of having that family size.  This shows that families have about one child on average.

```python
mean_pmf = 0
for x, p in pmf.Items():
    mean_pmf += x * p
print(mean_pmf)

1.024205155043831
```

We can do the same for the biased pmf.  Our results are skewed towards having children because the probability of having zero children is biased at zero.

```python
print(biased_pmf.Mean())
2.403679100664282
```
