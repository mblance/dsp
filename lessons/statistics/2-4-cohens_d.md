[Think Stats Chapter 2 Exercise 4](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#toc24) (Cohen's d)

Cohen's d allows us to compare two differernt populations by subtracting their means and dividing them by the pooled standard deviation.  This will tell us the effect size between the two populations.  A large value for cohen's D would indicate that the difference in the two mean's standard deviations is significant.  A small value would indicate that the two populations have almost no difference, or that the sample size is too small to draw a conclusion if you expected more significant results.

```python
import math
def cohend(pop1, pop2):
    diff = pop1.mean() - pop2.mean()
    var1, var2 = x1_pop.var(), x2_pop.var()
    n1, n2 = len(x1_pop), len(x2_pop)
    return diff / math.sqrt((n1 * var1 + n2 * var2) / (n1 + n2) )
```

We filter for live births by checking the value of outcome.  Then we compare the first live birth to all the other live births total weight in lbs (totalwgt_lb).  This field is derived by adding birthwgt_oz converted to lbs to birthwgt_lbs.  The effect size of birthorder on totalwgt_lb appears to be very small, well under the standard deviations of both populations.

```python
import nsfg
nsfg.CleanFemPreg(preg)
live = preg[preg.outcome == 1]

first = live[live.birthord == 1.0]
other = live[live.birthord != 1.0]
print(cohend(first.totalwgt_lb, other.totalwgt_lb))
print(first.totalwgt_lb.std(), other.totalwgt_lb.std())

-0.088672927072602
1.4205728777207374 1.394195476214313
```

We also see that there is a low effect size on pregnancy length

```python
print(cohend(first.prglngth, other.prglngth))
print(first.prglngth.std(), other.prglngth.std())

0.028879044654449883
2.7919014146686947 2.615852350439255
```
