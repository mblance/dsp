[Think Stats Chapter 8 Exercise 3](http://greenteapress.com/thinkstats2/html/thinkstats2009.html#toc77)

The function RunSimulation is called with games=5 for computing the mean.  We expect lam=5, or 5 goals per game on average.  The RMSE and mean error are calculated from the means of 1000 iterations.

```python
def SimulateGame(lam):
    """Simulates a game and returns the estimated goal-scoring rate.

    lam: actual goal scoring rate in goals per game
    """
    goals = 0
    t = 0
    while True:
        time_between_goals = random.expovariate(lam)
        t += time_between_goals
        if t > 1:
            break
        goals += 1

    # estimated goal-scoring rate is the actual number of goals scored
    L = goals
    return L

def RunSimulation(lam=5, games=5, iter=1000):
    means = []
    for i in range(iter):
        goals = []
        for i in range(games):
            goals.append(SimulateGame(lam))
        means.append(np.mean(goals))

    print('rmse', RMSE(means, lam))
    print('mean error', MeanError(means, lam))

RunSimulation()

rmse L 1.0177622512158722
mean error L 0.0020000000000000035
```

As we increase the number of games to 100 our RMSE and mean error approach zero.  We can say that this selection is unbiased.

```python
RunSimulation(games=200, iter=1000)
rmse 0.15632306291779213
mean error -0.011900000000000006
```
